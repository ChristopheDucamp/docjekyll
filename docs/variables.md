---
layout: docs
title: Variables
prev_section: pages
next_section: datafiles
permalink: /docs/variables/
---

Jekyll parcourt votre site en cherchant les fichiers à traiter. Tous les fichiers avec un [Front Matter YAML](../frontmatter/) sont sujets au traitement. Pour chacun de ces fichiers, Jekyll produit une variété de data disponibles via le [sytème de template Liquid](http://wiki.shopify.com/Liquid). 
Ce qui suit est une référence des data disponibles.

## Variables Globales 

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
      <td><p><code>site</code></p></td>
      <td><p>

          Information sur tout le site + réglages de configuration à partir du fichier 
          <code>_config.yml</code>. Voir en-dessous pour les détails.

      </p></td>
    </tr>
    <tr>
      <td><p><code>page</code></p></td>
      <td><p>

        Information spécifique à la page + le <a href="../frontmatter/">Front Matter YAML </a>. Les variables personnalisées réglées via le front matter YAML seront disponibles ici. Voir ci-dessous pour les détails.
      </p></td>
    </tr>
    <tr>
      <td><p><code>content</code></p></td>
      <td><p>

        Dans les fichiers layout, le contenu restitué du Post ou de la Page étant emballé. Non défini dans les fichiers Post ou Page.

      </p></td>
    </tr>
    <tr>
      <td><p><code>paginator</code></p></td>
      <td><p>

        Quand l'option de configuration <code>paginate</code> est réglée, cette variable devient disponible pour usage. Voir <a href="../pagination/">Pagination</a> pour les détails.

      </p></td>
    </tr>
  </tbody>
</table>
</div>

## Variables du Site

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
      <td><p><code>site.time</code></p></td>
      <td><p>

        L'heure actuelle (quand vous faites tourner la commande <code>jekyll</code>).

      </p></td>
    </tr>
    <tr>
      <td><p><code>site.pages</code></p></td>
      <td><p>

        Une liste de toutes les Pages.

      </p></td>
    </tr>
    <tr>
      <td><p><code>site.posts</code></p></td>
      <td><p>

        Une liste chronologique inversée de tous les Posts.

      </p></td>
    </tr>
    <tr>
      <td><p><code>site.related_posts</code></p></td>
      <td><p>

        Si la page en train d'être traitée est un Post, ceci contient une liste jusqu'à dix posts en rapport. Par défaut, ceux-ci sont de faible qualité mais rapides à traiter. Pour de la haute qualité mais lente pour traiter les résultats, faites tourner 
        <code>jekyll</code> command avec l'option <code>--lsi</code> (latent semantic
        indexing).

      </p></td>
    </tr>
    <tr>
      <td><p><code>site.categories.CATEGORY</code></p></td>
      <td><p>

        La liste de tous les Posts dans la catégorie <code>CATEGORY</code>.

      </p></td>
    </tr>
    <tr>
      <td><p><code>site.tags.TAG</code></p></td>
      <td><p>

        La liste de tous les Posts avec le tag <code>TAG</code>.

      </p></td>
    </tr>
    <tr>
      <td><p><code>site.[CONFIGURATION_DATA]</code></p></td>
      <td><p>

        Toutes les variables réglées via la ligne de commande et votre 
        <code>_config.yml</code> sont disponibles par la variable <code>site</code>. 
        Par exemple, si vous avez <code>url: http://monsite.com</code> 
        dans votre fichier de configuration, alors pour vos Posts et Pages, il sera stocké
        dans <code>site.url</code>. Jekyll ne parse pas les modifications de 
        <code>_config.yml</code> en mode <code>watch</code>, vous devez redémarrer Jekyll 
        pour voir les modifications faites aux variables.

      </p></td>
    </tr>
  </tbody>
</table>
</div>

## Variables de Page

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
      <td><p><code>page.content</code></p></td>
      <td><p>

        Le contenu non-traité de la Page.

      </p></td>
    </tr>
    <tr>
      <td><p><code>page.title</code></p></td>
      <td><p>

        Le titre de la Page.

      </p></td>
    </tr>
    <tr>
      <td><p><code>page.excerpt</code></p></td>
      <td><p>

        L'extrait non-rendu de la Page.

      </p></td>
    </tr>
    <tr>
      <td><p><code>page.url</code></p></td>
      <td><p>

        L'URL du Post sans le domaine, mais avec un slash en tête, par ex.
        <code>/2008/12/14/mon-post.html</code>

      </p></td>
    </tr>
    <tr>
      <td><p><code>page.date</code></p></td>
      <td><p>

        La Date assignée au Post. Ceci peut être écrasé dans un front matter de Post en spécifiant un nouveau date/time dans le format
        <code>AAAA-MM-JJ HH:MM:SS</code> (en supposant  UTC), ou
        <code>AAAA-MM-JJ HH:MM:SS +/-TTTT</code> (pour spécifier une zone horaire en utilisant un décalage à partir d'UTC par ex. <code>2008-12-14 10:30:00 +0900</code>).

      </p></td>
    </tr>
    <tr>
      <td><p><code>page.id</code></p></td>
      <td><p>

        Un identifiant unique vers le Post (utilisé dans les flux RSS). Par ex.
        <code>/2008/12/14/mon-post</code>

      </p></td>
    </tr>
    <tr>
      <td><p><code>page.categories</code></p></td>
      <td><p>

        La liste des catégories vers laquelle ce post appartient. Les catégories sont dérivées à partir de la structure de répertoire au-dessus du répertoire  <code>_posts</code>
        directory. Par exemple, un post sur 
        <code>/work/code/_posts/2008-12-24-closures.md</code> aurait ce champ réglé sur <code>['work', 'code']</code>. Ceux-ci peuvent être aussi spécifiés dans le <a href="../frontmatter/">YAML Front Matter</a>.

      </p></td>
    </tr>
    <tr>
      <td><p><code>page.tags</code></p></td>
      <td><p>

        La liste des tags à laquelle ce post appartient. Celles-ci peuvent être spécifiées dans le <a href="../frontmatter/">Front MatterYAML</a>.

      </p></td>
    </tr>
    <tr>
      <td><p><code>page.path</code></p></td>
      <td><p>

        Le chemin vers le post brut ou la page. Exemple d'usage : produire un lien retour vers la page ou la source du post sur GitHub. Ceci peut être écrasé dans le
        <a href="../frontmatter/">YAML Front Matter</a>.

      </p></td>
    </tr>
  </tbody>
</table>
</div>

<div class="note">
  <h5>ProTip™ : Utiliser un front-matter personnalisé</h5>
  <p>

    Tout front matter personnalisé que vous spécifiez sera disponible sous 
    <code>page</code>. Par exemple, si vous spécifiez  <code>custom_css: true</code>
    dans un front matter de page, cette valeur sera disponible sous 
    <code>page.custom_css</code>.

  </p>
</div>

## Paginator

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
      <td><p><code>paginator.per_page</code></p></td>
      <td><p>Nombre de Posts par page.</p></td>
    </tr>
    <tr>
      <td><p><code>paginator.posts</code></p></td>
      <td><p>Posts disponibles pour cette page.</p></td>
    </tr>
    <tr>
      <td><p><code>paginator.total_posts</code></p></td>
      <td><p>Nombre total de posts.</p></td>
    </tr>
    <tr>
      <td><p><code>paginator.total_pages</code></p></td>
      <td><p>Nombre total de Pages.</p></td>
    </tr>
    <tr>
      <td><p><code>paginator.page</code></p></td>
      <td><p>Le numéro de la page en cours.</p></td>
    </tr>
    <tr>
      <td><p><code>paginator.previous_page</code></p></td>
      <td><p>Le numéro de la page précédente.</p></td>
    </tr>
    <tr>
      <td><p><code>paginator.previous_page_path</code></p></td>
      <td><p>Le chemin vers la page précédente.</p></td>
    </tr>
    <tr>
      <td><p><code>paginator.next_page</code></p></td>
      <td><p>Le numéro de la page suivante.</p></td>
    </tr>
    <tr>
      <td><p><code>paginator.next_page_path</code></p></td>
      <td><p>Le chemin vers la prochaine page.</p></td>
    </tr>
  </tbody>
</table>
</div>

<div class="note info">
  <h5>Disponibilité de variable paginator</h5>
  <p>

    Celles-ci sont uniquement disponibles dans les fichiers index, néanmoins elles peuvent être situées dans un sous-répertoire, comme dans <code>/blog/index.html</code>.

  </p>
</div>
