---
layout: docs
title: Pagination
prev_section: permalinks
next_section: plugins
permalink: /docs/pagination/
---

Sur beaucoup de sites web —tout spécialement les blogs— il est courant de diviser la liste principale des posts en listes plus petites et de les afficher sur plusieurs pages. Jekyll a une pagination intégrée, ainsi vous pouvez générer automatiquement des listes paginées pour les fichiers et dossiers appropriés dont vous avez besoin.

<div class="note info">
  <h5>La pagination ne fonctionne que pour des fichiers HTML</h5>
  <p>
    La pagination ne fonctionne pas avec les fichiers Markdown ou Textile dans votre site Jekyll. Elle ne fonctionnera que quand elle est utilisée dans des fichiers HTML. Vous utiliserez probablement ça pour la liste des Posts, ceci ne devrait donc pas poser de problème.
  </p>
</div>

## Permettre la pagination

Pour permettre la pagination de votre blog, ajoutez une ligne au fichier `_config.yml` qui spécifie combien d'items devraient être affichés par page :

{% highlight yaml %}
paginate: 5
{% endhighlight %}

Le nombre devrait être le maximum de Posts par-page que vous aimeriez afficher dans le site généré.

Vous pouvez aussi spécifier la destination de la pagination : 

{% highlight yaml %}
paginate_path: "blog/page:num"
{% endhighlight %}

Ceci lira dans le fichier `blog/index.html`, enverra chaque page de pagination dans Liquid comme `paginator`
et écrira le rendu sur `blog/page:num`, où `:num` est le numéro de pagination de la page, commençant par `2`. Si un site a 12 posts et spécifie `paginate: 5`, Jekyll écrira `blog/index.html` avec les 5 premiers posts, `blog/page2/index.html` avec les 5 posts suivants et `blog/page3/index.html` avec les 2 derniers posts à l'intérieur du répertoire de destination.

## Attributs Liquid Disponibles

Le plugin de pagination expose l'objet liquid `paginator` avec les attributs suivants :

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>Attribut</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p><code>page</code></p></td>
      <td><p>numéro de la page en cours</p></td>
    </tr>
    <tr>
      <td><p><code>per_page</code></p></td>
      <td><p>nombre de posts par page</p></td>
    </tr>
    <tr>
      <td><p><code>posts</code></p></td>
      <td><p>une liste des posts pour la page en cours</p></td>
    </tr>
    <tr>
      <td><p><code>total_posts</code></p></td>
      <td><p>nombre total de posts dans le site</p></td>
    </tr>
    <tr>
      <td><p><code>total_pages</code></p></td>
      <td><p>nombre de pages de pagination</p></td>
    </tr>
    <tr>
      <td><p><code>previous_page</code></p></td>
      <td>
          <p>
              numéro de page de la page de pagination précédente,
              ou <code>nil</code> si aucune page précédente n'existe
          </p>
      </td>
    </tr>
    <tr>
      <td><p><code>previous_page_path</code></p></td>
      <td>
          <p>
              chemin de la page de pagniation précédente,
              ou <code>nil</code> si aucune page précédente n'existe
          </p>
      </td>
    </tr>
    <tr>
      <td><p><code>next_page</code></p></td>
      <td>
          <p>
              numéro de page de la page de pagination suivante,
              ou <code>nil</code> si aucune suivante n'existe
          </p>
      </td>
    </tr>
    <tr>
      <td><p><code>next_page_path</code></p></td>
      <td>
          <p>
              chemin de la page de pagination suivante,
              ou <code>nil</code> si aucune suivante n'existe
          </p>
      </td>
    </tr>
  </tbody>
</table>
</div>

<div class="note info">
  <h5>Pagination ne supporte pas les tags ou categories</h5>
  <p>Pagination pagine à travers chaque post dans la variable <code>posts</code>
  sans prendre en compte les variables définies dans le Front Matter YAML de chacun d'eux. 
  Il ne permet pas à cette heure de paginer des groupes de posts liés par un tag ou une catégorie communs.</p>
</div>

## Restituer les Posts Paginés

Le truc à savoir si vous avez besoin de faire ça, c'est afficher véritablement vos posts dans une liste en utilisant la variable `paginator` qui sera maintenant disponible. Vous voudrez probablement faire ça dans l'une des pages principales de votre site. Voici un exemple simple pour restituer des Posts paginés dans un fichier HTML : 

{% highlight html %}
{% raw %}
---
layout: default
title: Mon Blog
---

<!-- Ceci boucle a travers les posts pagines -->
{% for post in paginator.posts %}
  <h1><a href="{{ post.url }}">{{ post.title }}</a></h1>
  <p class="author">
    <span class="date">{{ post.date }}</span>
  </p>
  <div class="content">
    {{ post.content }}
  </div>
{% endfor %}

<!-- Liens de pagination -->
<div class="pagination">
  {% if paginator.previous_page %}
    <a href="/page{{ paginator.previous_page }}" class="previous">Avant</a>
  {% else %}
    <span class="previous">Avant</span>
  {% endif %}
  <span class="page_number ">Page : {{ paginator.page }} de {{ paginator.total_pages }}</span>
  {% if paginator.next_page %}
    <a href="/page{{ paginator.next_page }}" class="next">Suivant</a>
  {% else %}
    <span class="next ">Suivant</span>
  {% endif %}
</div>
{% endraw %}
{% endhighlight %}

<div class="note warning">
  <h5>Attention au cas isolé de la page un</h5>
  <p>
    Jekyll ne génère pas un dossier ‘page1’, par conséquent le code ci-dessus ne fonctionnera pas quand un lien <code>/page1</code> est produit. Voir en-dessous pour un moyen de gérer ça si c'est un problème pour vous.
  </p>
</div>

Le fragment HTML qui suit devrait gérer la page un, et restituer une liste avec des liens pour tout sauf la page en cours.

{% highlight html %}
{% raw %}
{% if paginator.total_pages > 1 %}
<div class="pagination">
  {% if paginator.previous_page %}
    <a href="{{ paginator.previous_page_path | prepend: site.baseurl | replace: '//', '/' }}">&laquo; Avant</a>
  {% else %}
    <span>&laquo; Avant</span>
  {% endif %}

  {% for page in (1..paginator.total_pages) %}
    {% if page == paginator.page %}
      <em>{{ page }}</em>
    {% elsif page == 1 %}
      <a href="{{ '/index.html' | prepend: site.baseurl | replace: '//', '/' }}">{{ page }}</a>
    {% else %}
      <a href="{{ site.paginate_path | prepend: site.baseurl | replace: '//', '/' | replace: ':num', page }}">{{ page }}</a>
    {% endif %}
  {% endfor %}

  {% if paginator.next_page %}
    <a href="{{ paginator.next_page_path | prepend: site.baseurl | replace: '//', '/' }}">Suivant &raquo;</a>
  {% else %}
    <span>Suivant &raquo;</span>
  {% endif %}
</div>
{% endif %}
{% endraw %}
{% endhighlight %}
