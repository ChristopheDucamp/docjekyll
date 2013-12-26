---
layout: docs
title: Structure des Répertoires
prev_section: usage
next_section: configuration
permalink: /docs/structure/
---

Jekyll, en son coeur, est un moteur de transformation de texte. Le concept derrière le système est celui-ci : vous lui donnez du texte écrit dans votre langage de marquage favori, que ce soit Markdown, Textile ou tout simplement du HTML, et il mixe cela à travers un layout ou une série de fichiers de layout. Par ce processus, vous pouvez bricoler comme vous voulez les URLs du site à regarder, quelles sont les data affichées dans le layout et bien plus encore. Tout ceci est produit à travers l'édition de fichiers textes, le site web statique étant le produit final.

Un site Jekyll basique ressemble généralement à ça : 

{% highlight bash %}
.
├── _config.yml
├── _drafts
|   ├── commence-avec-les-idees-folles.textile
|   └── de-la-simplicite-dans-la-techonologie.markdown
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   └── post.html
├── _posts
|   ├── 2013-10-29-pourquoi-chaque-programmeur-devrait-jouer-avec-indieweb.textile
|   └── 2013-04-26-indieweb-paris-.textile
├── _data
|   └── membres.yml
├── _site
└── index.html
{% endhighlight %}

Un aperçu de ce que chacun de ces items produit :

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>Fichier / Répertoire</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p><code>_config.yml</code></p>
      </td>
      <td>
        <p>

          Stocke les data de <a href="../configuration/">configuration</a>. Bon nombre de ces options peuvent être spécifiées à partir de l'exécutable en ligne de commande mais il est plus facile de les spécifier ici pour que vous puissiez vous en souvenir.

        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>_drafts</code></p>
      </td>
      <td>
        <p>

          Les drafts sont des posts non publiés. Le format de ces fichiers est sans date : <code>title.MARKUP</code>. Apprenez comment <a href="../drafts/">travailler avec des drafts</a>.

        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>_includes</code></p>
      </td>
      <td>
        <p>

          Ceci sont des partiels qui peuvent être mixés et reconnus par vos layouts et posts pour réutilisation. Le tag liquid 
          <code>{% raw %}{% include file.ext %}{% endraw %}</code>
          peut être utilisé pour inclure le partiel dans <code>_includes/file.ext</code>.

        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>_layouts</code></p>
      </td>
      <td>
        <p>

          Voici les templates qui emballent les posts. Les layouts sont choisis sur une base post-à-post dans le <a href="../frontmatter/">front matter YAML</a>, décrit dans la section suivantes. Le tag liquid
          <code>{% raw %}{{ content }}{% endraw %}</code>
          est utilisé pour injecter du contenu à l'intérieur de la page web.

        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>_posts</code></p>
      </td>
      <td>
        <p>

          Votre contenu dynamique, pour ainsi dire. Le format de ces fichiers est important, et doit suivre le format :
          <code>ANNEE-MOIS-JOUR-title.MARKUP</code>.
          Les <a href="../permalinks/">permaliens</a> peuvent être personnalisés pour chaque post, mais la date et le langage de marquage sont déterminés uniquement par le nom de fichier.

        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>_data</code></p>
      </td>
      <td>
        <p>

          La data du site bien formatée devrait être placée ici. Le moteur Jekyll auto-chargera tous les fichiers yaml (fin avec <code>.yml</code> ou <code>.yaml</code>) dans ce répertoire. S'il existe un fichier <code>membres.yml</code> sous le répertoire, alors vous pouvez accéder aux contenus du fichiers à travers<code>site.data.membres</code>.

        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>_site</code></p>
      </td>
      <td>
        <p>

          C'est là où le site généré sera placé (par défaut) une fois que Jekyll a effectué la transformation. C'est probablement une bonne idée de l'ajouter à votre fichier <code>.gitignore</code>.

        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>index.html</code> et d'autres fichiers HTML, Markdown, Textile</p>
      </td>
      <td>
        <p>

          Si le fichier a une section <a href="../frontmatter/">YAML Front
          Matter</a>, il sera transformé par Jekyll. La même chose arrive pour tout fichier <code>.html</code>, <code>.markdown</code>,
          <code>.md</code>, ou <code>.textile</code> dans le répertoire racine de votre site ou les répertoires non listées au-dessus.

        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>Autres fichiers/Répertoires</p>
      </td>
      <td>
        <p>

          Chaque autre répertoire et fichier mis à part ceux listés au-dessus- tels que des dossiers  
          <code>css</code> et <code>images</code>, des fichiers <code>favicon.ico</code>, et ainsi de suite seront copiés vers le site généré. Il existe beaucoup de <a href="../sites/">sites utilisant déjà Jekyll</a>  si vous êtes curieux de voir comment ils sont construits.

        </p>
      </td>
    </tr>
  </tbody>
</table>
</div>
