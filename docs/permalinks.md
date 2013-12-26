---
layout: docs
title: Permaliens
prev_section: templates
next_section: pagination
permalink: /docs/permalinks/
---

Jekyll supporte un moyen flexible pour construire les URLs de votre site. Vous pouvez spécifier les permaliens de votre site dans la [Configuration](../configuration/) ou dans le 
[Front Matter YAML](../frontmatter/) pour chaque post. Vous êtes libre de choisir l'un des styles intégrés pour créer vos liens ou façonner les vôtres. Le style par défaut est `date`.

Les permaliens sont construits en créant un gabarit d'URL où les éléments dynamiques sont représentés par des mots-clés préfixés-par-deux-points. Par exemple, le permalien par défaut `date` est défini comme  `/:categories/:year/:month/:day/:titre.html`.

## Variables template

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
        <p><code>year</code></p>
      </td>
      <td>
        <p>Année extraite du nom de fichier du Post</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>month</code></p>
      </td>
      <td>
        <p>Mois extrait du nom de fichier du Post</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>i_month</code></p>
      </td>
      <td>
        <p>Mois tiré du nom de fichier du Post sans les zéros devant.</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>day</code></p>
      </td>
      <td>
        <p>Jour extrait du nom de fichier du Post</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>i_day</code></p>
      </td>
      <td>
        <p>Jour extrait du nom de fichier du Post sans les zéros devant.</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>title</code></p>
      </td>
      <td>
        <p>Titre extrait du nom de fichier du Post</p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>categories</code></p>
      </td>
      <td>
        <p>
          Les catégories spécifiées pour ce Post. Jekyll parse automatiquement les double slashes dans les URLs, aussi si aucune catégorie n'est présente, il ignorera cela.
        </p>
      </td>
    </tr>
  </tbody>
</table>
</div>

## Styles de permaliens intégrés

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>Style de Permalien</th>
      <th>Gabarit URL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p><code>date</code></p>
      </td>
      <td>
        <p><code>/:categories/:year/:month/:day/:title.html</code></p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>pretty</code></p>
      </td>
      <td>
        <p><code>/:categories/:year/:month/:day/:title/</code></p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>none</code></p>
      </td>
      <td>
        <p><code>/:categories/:title.html</code></p>
      </td>
    </tr>
  </tbody>
</table>
</div>

## Exemples de style de permalien

Prenons un post appelé : `/2009-04-29-crac-boum.textile`

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>Réglage Permalien</th>
      <th>URL Permalien Résultante</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p>Rien de spécifié, ou <code>permalink: date</code></p>
      </td>
      <td>
        <p><code>/2009/04/29/crac-boum.html</code></p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>permalink: pretty</code></p>
      </td>
      <td>
        <p><code>/2009/04/29/crac-boum/index.html</code></p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>permalink: /:month-:day-:year/:title.html</code></p>
      </td>
      <td>
        <p><code>/04-29-2009/crac-boum.html</code></p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>permalink: /blog/:year/:month/:day/:title</code></p>
      </td>
      <td>
        <p><code>/blog/2009/04/29/crac-boum/index.html</code></p>
      </td>
    </tr>
  </tbody>
</table>
</div>
