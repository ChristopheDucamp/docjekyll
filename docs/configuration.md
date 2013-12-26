---
layout: docs
title: Configuration
prev_section: structure
next_section: frontmatter
permalink: /docs/configuration/
---

Jekyll vous permet de concocter vos sites comme vous en avez rêvé, et ceci grâce aux options puissantes et flexibles de configurations qui rendent cela possible. Ces options peuvent être spécifiées soit dans un fichier `_config.yml` placé dans le répertoire racine de votre site, ou directement dans le terminal sous forme d'instructions pour l'exécutable `jekyll`.

## Paramètres de Configuration

### Configuration Globale

Le tableau ci-dessous liste les réglages disponibles pour Jekyll, et les différentes <code class="option">options</code> (spécifiées dans le fichier de configuration) et les <code class="flag">flags</code> (spécifiées sur la ligne de commande) qui les contrôlent.

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>Réglage</th>
      <th>
        <span class="option">Options</span> et <span class="flag">Flags</span>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Site Source</strong></p>
        <p class='description'>Modifie le répertoire où Jekyll lira les fichiers</p>
      </td>
      <td class="align-center">
        <p><code class="option">source: DIR</code></p>
        <p><code class="flag">-s, --source DIR</code></p>
      </td>
    </tr>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Site de Destination</strong></p>
        <p class='description'>Modifie le répertoire où Jekyll écrira les fichiers </p>
      </td>
      <td class="align-center">
        <p><code class="option">destination: DIR</code></p>
        <p><code class="flag">-d, --destination DIR</code></p>
      </td>
    </tr>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Sécurité</strong></p>
        <p class='description'>Désactive les <a href="../plugins/">plugins personnalisés</a>.</p>
      </td>
      <td class="align-center">
        <p><code class="option">safe: BOOL</code></p>
        <p><code class="flag">--safe</code></p>
      </td>
    </tr>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Exclure</strong></p>
        <p class="description">Exclure les répertoires et/ou les fichiers à partir de la conversion</p>
      </td>
      <td class='align-center'>
        <p><code class="option">exclude: [DIR, FILE, ...]</code></p>
      </td>
    </tr>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Inclure</strong></p>
        <p class="description">
          Force l'inclusion de répertoires et/ou fichiers dans la conversion. 
          <code>.htaccess</code> est un bon exemple parce que les fichiers à point sont exclus par défaut.
        </p>
      </td>
      <td class='align-center'>
        <p><code class="option">include: [DIR, FILE, ...]</code></p>
      </td>
    </tr>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Fuseau Horaire</strong></p>
        <p class="description">
            Règle la zone horaire. Ceci régle la variable d'environnement <code>TZ</code> que Ruby utilise pour gérer la création et la manipulation de l'heure et la date. Toute entrée provenant de la <a href="http://en.wikipedia.org/wiki/Tz_database">Database IANA Time Zone</a> est valide, par ex. <code>America/New_York</code>. La valeur par défaut est la zone horaire locale, telle que réglée par votre système d'exploitation.
        </p>
      </td>
      <td class='align-center'>
        <p><code class="option">timezone: TIMEZONE</code></p>
      </td>
    </tr>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Encodage</strong></p>
        <p class="description">
            Règle l'encodage des fichiers par nom. Seulement disponible pour Ruby
            1.9 ou suivante).
            La valeur par défaut est nil, qui utilise la valeur par défaut de Ruby,
            <code>ASCII-8BIT</code>.
            L'encodage disponible pour le ruby en utilisation, peut être affiché par la commande 
            <code>ruby -e 'puts Encoding::list.join("\n")'</code>
        </p>
      </td>
      <td class='align-center'>
        <p><code class="option">encoding: ENCODING</code></p>
      </td>
    </tr>
  </tbody>
</table>
</div>

### Options de la Commande Build

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>Réglage</th>
      <th><span class="option">Options</span> et <span class="flag">Flags</span></th>
    </tr>
  </thead>
  <tbody>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Régéneration</strong></p>
        <p class='description'>Permet l'auto-régénération du site quand les fichiers sont modifiés.</p>
      </td>
      <td class="align-center">
        <p><code class="flag">-w, --watch</code></p>
      </td>
    </tr>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Configuration</strong></p>
        <p class="description">Spécifie les fichiers de config au lieu d'utiliser <code>_config.yml</code> automatiquement. Les réglages dans les fichiers ultérieurs écraseront les réglages dans les fichiers plus anciens.</p>
      </td>
      <td class='align-center'>
        <p><code class="flag">--config FILE1[,FILE2,...]</code></p>
      </td>
    </tr>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Drafts</strong></p>
        <p class="description">Processus et rendu des posts brouillons.</p>
      </td>
      <td class='align-center'>
        <p><code class="flag">--drafts</code></p>
      </td>
    </tr>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Futur</strong></p>
        <p class="description">Publie les posts avec une date future.</p>
      </td>
      <td class='align-center'>
        <p><code class="option">future: BOOL</code></p>
        <p><code class="flag">--future</code></p>
      </td>
    </tr>
    <tr class='setting'>
      <td>
        <p class='name'><strong>LSI</strong></p>
        <p class="description">Produit un index pour les posts en rapport.</p>
      </td>
      <td class='align-center'>
        <p><code class="option">lsi: BOOL</code></p>
        <p><code class="flag">--lsi</code></p>
      </td>
    </tr>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Limitation des Posts</strong></p>
        <p class="description">Limite le nombre de posts à analyser et publier.</p>
      </td>
      <td class='align-center'>
        <p><code class="option">limit_posts: NUM</code></p>
        <p><code class="flag">--limit_posts NUM</code></p>
      </td>
    </tr>
  </tbody>
</table>
</div>

### Options de la Commande Serve

En plus des options ci-dessous, la sous-commande `serve` peut accepter n'importe quelle option pour la sous-commande `build`, des options qui sont alors appliquées à la construction du site qui se déroule juste avant que votre site ne soit servi.

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>Réglage</th>
      <th><span class="option">Options</span> et <span class="flag">Flags</span></th>
    </tr>
  </thead>
  <tbody>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Local Server Port</strong></p>
        <p class='description'>Écoute le port donné.</p>
      </td>
      <td class="align-center">
        <p><code class="option">port: PORT</code></p>
        <p><code class="flag">--port PORT</code></p>
      </td>
    </tr>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Local Server Hostname</strong></p>
        <p class='description'>Écoute le nom d'hôte donné.</p>
      </td>
      <td class="align-center">
        <p><code class="option">host: HOSTNAME</code></p>
        <p><code class="flag">--host HOSTNAME</code></p>
      </td>
    </tr>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Base URL</strong></p>
        <p class='description'>Sert le site web à partir de l'URL de base donnée</p>
      </td>
      <td class="align-center">
        <p><code class="option">baseurl: URL</code></p>
        <p><code class="flag">--baseurl URL</code></p>
      </td>
    </tr>
    <tr class='setting'>
      <td>
        <p class='name'><strong>Detach</strong></p>
        <p class='description'>Detach the server from the terminal</p>
      </td>
      <td class="align-center">
        <p><code class="option">detach: BOOL</code></p>
        <p><code class="flag">-B, --detach</code></p>
      </td>
    </tr>
  </tbody>
</table>
</div>

<div class="note warning">
  <h5>N'utilisez pas de tabulations dans les fichiers de configuration</h5>
  <p>
    Ceci conduira soit à des erreurs de parsage, ou Jekyll réinitiliasera les paramètres par défaut. Utilisez des espaces à la place.
  </p>
</div>

## Configuration par Défaut

Jekyll fonctionne par défaut avec les options de configuration qui suivent. A moins que des paramètres alternatifs pour ces options ne soient explicitement spécifiés dans le fichier de configuration ou sur la ligne de commande, Jekyll tournera en utilisant ces otpions.

<div class="note warning">
  <h5>Voici deux options  kramdown non supportées</h5>
  <p>
    Notez SVP qu'à la fois <code>remove_block_html_tags</code> et 
    <code>remove_span_html_tags</code> ne sont à cette heure pas supportés par Jekyll du fait qu'ils ne sont pas inclus dans le convertisseur HTML kramdown.
  </p>
</div>

{% highlight yaml %}
source:      .
destination: ./_site
plugins:     ./_plugins
layouts:     ./_layouts
include:     ['.htaccess']
exclude:     []
keep_files:  ['.git','.svn']
gems:        []
timezone:    nil
encoding:    nil

future:      true
show_drafts: nil
limit_posts: 0
pygments:    true

relative_permalinks: true

permalink:     date
paginate_path: 'page:num'

markdown:      maruku
markdown_ext:  markdown,mkd,mkdn,md
textile_ext:   textile

excerpt_separator: "\n\n"

safe:        false
watch:       false    # deprecated
server:      false    # deprecated
host:        0.0.0.0
port:        4000
baseurl:     /
url:         http://localhost:4000
lsi:         false

maruku:
  use_tex:    false
  use_divs:   false
  png_engine: blahtex
  png_dir:    images/latex
  png_url:    /images/latex
  fenced_code_blocks: true

rdiscount:
  extensions: []

redcarpet:
  extensions: []

kramdown:
kramdown:
  auto_ids: true
  footnote_nr: 1
  entity_output: as_char
  toc_levels: 1..6
  smart_quotes: lsquo,rsquo,ldquo,rdquo
  use_coderay: false

  coderay:
    coderay_wrap: div
    coderay_line_numbers: inline
    coderay_line_numbers_start: 1
    coderay_tab_width: 4
    coderay_bold_every: 10
    coderay_css: style
    
redcloth:
  hard_breaks: true
{% endhighlight %}


## Options Markdown 

Les différents analyseurs Markdown supportés par défaut ont des options supplémentaires disponibles.

### Redcarpet

Redcarpet peut être configuré en fournissant un sous-réglage `extensions`, dont la valeur devrait être une  array de strings. Chaque chaîne devrait être le nom d'une des extensions de classes `Redcarpet::Markdown` ; si présent dans l'array, elle règlera dans l'extension correspondante à `true`.

Jekyll gère deux extensions spéciales Redcarpet :

- `no_fenced_code_blocks` --- Par défaut, Jekyll règle l'extension `fenced_code_blocks` (pour délimiter les blocs de code avec trois tildes ou trois guillemets arrière) sur `true`, probablement parce que l'adoption de GitHub commence à les rendre inéchappables. L'extension normale de Redcarpet `fenced_code_blocks` est inerte quand elle est utilisée avec Jekyll ; au lieu de cela, vous pouvez utiliser cette version inversée de l'extension pour désactiver le code clos.

    Notez que vous pouvez aussi spécifier un langage pour mettre en valeur après le premier délimiteur :

        ```ruby
        # ...ruby code
        ```

    Avec à la fois les blocs de code entourés et pygments autorisé, ceci mettra statiquement en valeur le code ; sans pygments, ceci ajoutera un attribut `class="LANGUAGE"` à l'élément `<code>`, qui peut être utilisé comme un truc par différentes bibliothèques JavaScript pour mettre en avant le code.
- `smart` --- Cette pseudo-extension fonctionne sur SmartyPants, qui convertit les citations directes en guillemets élégants et qui convertit les citations droites en guillemets inclinés et transforme les soulignés en em (`---`) et les tirets (`--`) en ?.

Toutes les autres extensions conservent leurs noms usuels à partir de RedCarpet, and aucune option de rendu hormis `smart` ne peut être spécifiée dans Jekyll. [Une liste d'extensions disponibles peut être trouvée dans le fichier README de Redcarpet.][redcarpet_extensions] Assurez-vous que vous regardez bien la bonne version de Redcarpet : Jekyll utilise actuellement la v2.2.x, et les extensions comme `footnotes` et  `highlight` n'ont pas été ajoutées après la version 3.0.0. Les extensions les plus communément utilisées sont : 

- `tables`
- `no_intra_emphasis`
- `autolink`

[redcarpet_extensions]: https://github.com/vmg/redcarpet/blob/v2.2.2/README.markdown#and-its-like-really-simple-to-use

### Kramdown

En plus de valeurs par défaut citées au-dessus, vous pouvez aussi activer la reconnaissance de Github Flavored Markdown en passant une option `input` avec une valeur de "GFM".

Par exemple, dans votre fichier `_config.yml`:

    kramdown:
      input: GFM
