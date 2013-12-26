---
layout: docs
title: Front-matter
prev_section: configuration
next_section: posts
permalink: /docs/frontmatter/
---

Le front-matter est l'endroit où Jekyll commence à être vraiment cool. Tout fichier contenant un bloc [YAML](http://yaml.org/) front matter sera traité par Jekyll comme un fichier spécial. Le front matter doit être la première chose dans le fichier et doit prendre la forme d'un ensemble YAML valide placé avec trois tirets. Voici un exemple basique :


{% highlight yaml %}
---
layout: post
title: Bloguer Comme un Hacker
---
{% endhighlight %}

Entre ces trois tirets ('`-`'), vous pouvez régler des variables prédéfinies (voir en dessous pour une référence) ou même créer vos propres règles personnalisées. Ces variables seront ensuite disponibles pour y accéder en utilisant des marqueurs Liquid tant dans le fichier que  dans n'importe lesquels des layouts ou des includes dont dépend la page ou le post en question.

<div class="note warning">
  <h5>Attention à l'Encodage de Caractère UTF-8</h5>
  <p>
    Si vous utilisez l'encodage UTF-8, assurez-vous qu'aucun caractère header <code>BOM</code> n'existe dans vos fichiers, sinon de très très mauvaises choses se passeront dans Jekyll. Ceci est tout particulièrement avéré si vous faites tourner Jekyll sur Windows.
  </p>
</div>

<div class="note">
  <h5>ProTruc™ : Les Variables Front Matter Sont Optionnelles</h5>
  <p>
    Si vous voulez utiliser les <a href="../variables/">tags Liquid et des variables</a> mais n'avez pas besoin de quoi que ce soit dans votre front-matter, laissez-le simplement vide ! L'ensemble des lignes entre les trois tirets avec rien entre eux amènera Jekyll à traiter votre fichier. (Ceci peut être utile pour des choses comme les CSS et flux RSS !)
  </p>
</div>

## Variables Globales Prédéfinies

Il existe un certain nombre de variables pré-définies que vous pouvez régler dans le front-matter d'une page ou d'un post.

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p><code>layout</code></p>
      </td>
      <td>
        <p>

          Si réglé, ceci spécifie le fichier de layout à utiliser. Utilisez le nom du fichier layout sans l'extension du fichier. Les fichiers de layout doivent être placés dans le répertoire 
          <code>_layouts</code>.

        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>permalink</code></p>
      </td>
      <td>
        <p>

          Si vous avez besoin que vos URLs traitées de posts de blog soient quelque chose d'autre que l'option par défaut <code>/année/mois/jour/titre.html</code> alors vous pouvez régler cela et ce sera utilisé comme l'URL finale.

        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>published</code></p>
      </td>
      <td>
        <p>
          Réglez cela sur false, si vous ne voulez pas qu'un post spécifique s'affiche quand le post est généré. </p>
      </td>
    </tr>
    <tr>
      <td>
        <p style="margin-bottom: 5px;"><code>category</code></p>
        <p><code>categories</code></p>
      </td>
      <td>
        <p>

          Au lieu de placer les posts à l'intérieur de répertoires, vous pouvez spécifier une ou plusieurs catégories à laquelle appartient le post. Quand le site est généré, le post se comportera comme s'il avait été  réglé normalement. Categories (pluriel) peut être spécifié sous forme de  <a
          href="http://fr.wikipedia.org/wiki/YAML#Listes">liste YAML</a> ou sous forme de chaîne séparée par des espaces.

        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>tags</code></p>
      </td>
      <td>
        <p>

          Similaire aux catégories, un ou plusieurs mots-clés peuvent être ajoutés à un post. Tout comme les catégories, les tags peuvent être spécifiés sous forme de liste YAML ou de chaîne séparée par des espaces.

        </p>
      </td>
    </tr>
  </tbody>
</table>
</div>


## Variables Personnalisées

Toutes les variables dans le front matter qui ne sont pas prédéfinies sont mixées à l'intérieur de la data envoyée au moteur de gabarit Liquid durant la conversion. Par exemple, si vous réglez un titre, vous pouvez utiliser ça dans votre layout pour régler le titre de la page :

{% highlight html %}
<!DOCTYPE HTML>
<html>
  <head>
    <title>{% raw %}{{ page.title }}{% endraw %}</title>
  </head>
  <body>
    ...
{% endhighlight %}

## Variables Prédéfinies pour les Posts

Celles-ci sont disponibles en sortie de boîte pour être utilisées dans le front-matter pour un post.


<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p><code>date</code></p>
      </td>
      <td>
        <p>
          Une date ici écrase la date du nom du post. Ceci peut être utilisé pour vosu assurer d'un tri correct des posts.
        </p>
      </td>
    </tr>
  </tbody>
</table>
</div>
