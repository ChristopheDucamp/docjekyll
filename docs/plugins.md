---
layout: docs
title: Plugins
prev_section: pagination
next_section: extras
permalink: /docs/plugins/
---

Jekyll a un système de plugin avec des hooks qui vous permettent du contenu spécifique à votre site. Vous pouvez faire tourner du code personnalisé pour votre site sans devoir modifier le source Jekyll.

<div class="note info">
  <h5>Plugins sur Pages GitHub</h5>
  <p>
    <a href="http://pages.github.com/">GitHub Pages</a> est motorisé par Jekyll,
    néanmoins tous les sites Pages sont générés en utilisant l'option <code>--safe</code> 
    pour désactiver les plugins personnalisés pour des raisons de sécurité. Malheureusement, ceci veut dire que 
    vos plugins ne fonctionneront pas si vous déployez vers un hébergement GitHub Pages.<br><br>
    Vous pouvez encore utiliser GitHub Pages pour publier votre site, mais vous devrez convertir le site localement 
    et pousser les fichiers statiques générés vers votre dépôt GitHub au lieu des fichiers source Jekyll.
  </p>
</div>

## Installer un plugin

Vous avez 2 options pour installer des plugins :

1. Dans votre racine de site source, créez un répertoire `_plugins`. Placez vos plugins dedans.
    Tout fichier se terminant par `*.rb` dans ce dossier sera chargé avant que Jekyll ne génère votre site.
2. Dans votre fichier `_config.yml`, ajoutez un nouvel array avec les `gems` clés et les valeurs des noms 
   des gems des plugins que vous aimeriez utiliser. Un exemple : 

        gems: [jekyll-test-plugin, jekyll-jsonify, jekyll-assets]
        # This will require each of these gems automatically.

<div class="note info">
  <h5>
    <code>_plugins</code> et <code>gems</code>
    peuvent être utilisés simultanément
  </h5>
  <p>
    Vous pouvez utiliser à la fois les options de plugin mentionnées plus haut simultanément dans le même 
    site si vous choisissez de faire ainsi. L'usage de l'un ne restreint pas l'usage de l'autre
  </p>
</div>

En général, les plugins que vous construisez tomberont dans l'une des trois catégories : 

1. Générateurs
2. Convertisseurs
3. Tags

## Générateurs

Vous pouvez créer un générateur quand vous voulez que Jekyll crée un contenu additionnel basé sur vos propres règles.

Un générateur est une sous-classe de `Jekyll::Generator` qui définit une méthode `generate`
qui reçoit une instance de 
[`Jekyll::Site`]({{ site.repository }}/blob/master/lib/jekyll/site.rb).

La génération est déclenchée par ses effets de bord, la valeur retour de `generate` est
ignorée. Jekyll ne suppose pas que toute effet de bord particulier arrive, il fait juste fonctionner la méthode.

Les générateurs fonctionnent après que Jekyll ait produit un inventaire du contenu existant, et avant que le site ne soit généré.
Les Pages avec des front-matters YAML sont stockées comme des instances de 
[`Jekyll::Page`]({{ site.repository }}/blob/master/lib/jekyll/page.rb)
et sont disponibles via `site.pages`. Les fichiers statiques deviennent des instances de 
[`Jekyll::StaticFile`]({{ site.repository }}/blob/master/lib/jekyll/static_file.rb)
et sont disponibles via `site.static_files`. Voir 
[`Jekyll::Site`]({{ site.repository }}/blob/master/lib/jekyll/site.rb)
pour plus de détails.

Par exemple, un générateur peut injecter des valeurs calculée sur le temps de construction pour des variables template. 
Dans l'exemple suivant le template `reading.html` a deux 
variables `ongoing` et `done` que nous remplissons dans le générateur : 

{% highlight ruby %}
module Reading
  class Generator < Jekyll::Generator
    def generate(site)
      ongoing, done = Book.all.partition(&:ongoing?)

      reading = site.pages.detect {|page| page.name == 'reading.html'}
      reading.data['ongoing'] = ongoing
      reading.data['done'] = done
    end
  end
end
{% endhighlight %}

Ceci est un générateur plus complexe qui génère de nouvelles pages :

{% highlight ruby %}
module Jekyll

  class CategoryPage < Page
    def initialize(site, base, dir, category)
      @site = site
      @base = base
      @dir = dir
      @name = 'index.html'

      self.process(@name)
      self.read_yaml(File.join(base, '_layouts'), 'category_index.html')
      self.data['category'] = category

      category_title_prefix = site.config['category_title_prefix'] || 'Category: '
      self.data['title'] = "#{category_title_prefix}#{category}"
    end
  end

  class CategoryPageGenerator < Generator
    safe true

    def generate(site)
      if site.layouts.key? 'category_index'
        dir = site.config['category_dir'] || 'categories'
        site.categories.keys.each do |category|
          site.pages << CategoryPage.new(site, site.source, File.join(dir, category), category)
        end
      end
    end
  end

end
{% endhighlight %}

Dans cet exemple, notre générateur créera une série de fichiers sous le 
répertoire `categories` pour chaque catégorie, listant les posts dans chaque catégorie
en utilisant le layout `category_index.html`.

Les générateurs exigent uniquement d'implémenter une méthode : 

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>Méthode</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p><code>generate</code></p>
      </td>
      <td>
        <p>Génère du contenu comme un effet de bord.</p>
      </td>
    </tr>
  </tbody>
</table>
</div>

## Convertisseurs

Si vous avez un nouveau langage de marquage que vous aimeriez utiliser sur votre site, vous pouvez l'ajouter en implémentant votre propre convertisseur. 
Les deux langages de marquage Markdown et Textile sont implémentés en utilisant cette méthode.

<div class="note info">
  <h5>Souvenez-vous de votre front-matter YAML</h5>
  <p>
    Jekyll ne convertira que les fichiers qui ont un en-tête YAML en haut, même pour les convertisseurs que vous ajoutez en utilisant un plugin.
  </p>
</div>

Ci-dessous un convertisseur qui prendra tous les posts se terminant par `.upcase` et les traitera en utilisant `UpcaseConverter`:

{% highlight ruby %}
module Jekyll
  class UpcaseConverter < Converter
    safe true
    priority :low

    def matches(ext)
      ext =~ /^\.upcase$/i
    end

    def output_ext(ext)
      ".html"
    end

    def convert(content)
      content.upcase
    end
  end
end
{% endhighlight %}

Les Convertisseurs devraient implémenter au minimum 3 méthodes : 

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>Méthode</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p><code>matches</code></p>
      </td>
      <td><p>
        Est-ce que l'extension donnée correspond à cette liste d'extensions acceptable de convertisseur ? 
        Prenez un argument : l'extension du fichier (y compris le point). Doit retourner 
        <code>true</code> si ça correspond, sinon <code>false</code>.
      </p></td>
    </tr>
    <tr>
      <td>
        <p><code>output_ext</code></p>
      </td>
      <td><p>
        L'extension à donner au fichier de sortie (y compris le point).
        Généralement ce sera <code>".html"</code>.
      </p></td>
    </tr>
    <tr>
      <td>
        <p><code>convert</code></p>
      </td>
      <td><p>
        Logique pour faire la conversion de contenu. Prend un argument : le contenu brut
        du fichier (sans le front matter YAML). Doit renvoyer une chaîne.
      </p></td>
    </tr>
  </tbody>
</table>
</div>

Dans notre exemple, `UpcaseConverter#matches` vérifie si notre extension de nom de fichier est 
`.upcase`, et sera restituée en utilisant le convertisseur s'il existe. Il appellera 
`UpcaseConverter#convert` pour traiter le contenu. Dans notre convertisseur simple, nous somme simplement en train 
de mettre en capitales la totalité de la chaîne de contenu. Pour finri, quand il sauvegarde la page, 
il fera ainsi avec une extension `.html`.

## Tags

Si vous aimeriez inclure des tags personnalisés liquid dans votre site, vous pouvez faire ainsi en 
hookant à l'intérieur du système de tag. Les exemples intégrés ajoutés par Jekyll incluent les tags 
`highlight` et `include`. Ci-dessous un exemple de tag personnalisé liquid qui produira l'heure à laquelle la page a 
été restituée :  

{% highlight ruby %}
module Jekyll
  class RenderTimeTag < Liquid::Tag

    def initialize(tag_name, text, tokens)
      super
      @text = text
    end

    def render(context)
      "#{@text} #{Time.now}"
    end
  end
end

Liquid::Template.register_tag('render_time', Jekyll::RenderTimeTag)
{% endhighlight %}

Au minimum, les tags liquide doivent implémenter : 

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>Méthode</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p><code>render</code></p>
      </td>
      <td>
        <p>Sort le contenu du tag.</p>
      </td>
    </tr>
  </tbody>
</table>
</div>

Vous devez aussi enregistrer le tag personnalisé avec le moteur de template Liquide comme suit : 

{% highlight ruby %}
Liquid::Template.register_tag('render_time', Jekyll::RenderTimeTag)
{% endhighlight %}

Dans l'exemple du dessus, nous pouvons placer le tag suivant dans l'une de nos pages : 

{% highlight ruby %}
{% raw %}
<p>{% page produite le : render_time %}</p>
{% endraw %}
{% endhighlight %}

Et nous obtiendrons quelque chose comme ça sur la page : 

{% highlight html %}
<p>page produite le : Tue June 22 23:38:47 –0500 2010</p>
{% endhighlight %}

### Filtres Liquid 

Vous pouvez ajouter vos propres filtres au système de template Liquid tout comme vous pouvez ajouter les tags au-dessus. 
Les filtres sont simplement des modules qui exportent leurs méthodes vers liquid. Toutes les 
méthodes devront avoir au moins un paramètre qui représente l'input du filtre. La valeur retour sera l'output du filtre.

{% highlight ruby %}
module Jekyll
  module AssetFilter
    def asset_url(input)
      "http://www.exemple.com/#{input}?#{Time.now.to_i}"
    end
  end
end

Liquid::Template.register_filter(Jekyll::AssetFilter)
{% endhighlight %}

<div class="note">
  <h5>ProTip™ : Accéder à l'objet du site en utilisant Liquid</h5>
  <p>
    Jekyll vous permet d'accéder à l'objet du <code>site</code> à travers la 
    fonctionnalité <code>context.registers</code> de Liquid sur <code>context.registers[:site]</code>. Par exemple, vous pouvez 
    accéder au fichier global de configuration <code>_config.yml</code> en utilisant 
    <code>context.registers[:site].config</code>.
  </p>
</div>

### Flags

Il existe deux flags à connaître au moment d'écrire un plugin : 

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>Flag</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p><code>safe</code></p>
      </td>
      <td>
        <p>
          Un flag booléen qui informe Jekyll si ce plugin peut être exécuté en toute sécurité 
          dans un environnement où l'exécution de code arbitraire n'est pas permise. 
          Ceci est utilisé par GitHub Pages pour déterminer quels plugins noyaux peuvent être 
          utilisés et quels sont ceux qui sont peu sûrs à faire fonctionner. Si votre plugin 
          ne permet pas d'exécution de code arbitraire, réglez ça sur <code>true</code>.
          GitHub Pages ne vous laissera néanmoins pas charger votre plugin, mais si vous le proposez 
          pour inclusion dans le noyau, il est préférable pour celui-ci d'être correct !
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>priority</code></p>
      </td>
      <td>
        <p>
          Ce flag détermine dans quel ordre le plugin est chargé. Les valeurs valide 
          sont : <code>:lowest</code>, <code>:low</code>, <code>:normal</code>,
          <code>:high</code>, et <code>:highest</code>. Les priorités les plus hautes 
          sont d'abord appliquées, les priorités les plus basses sont appliquées en dernier.
        </p>
      </td>
    </tr>
  </tbody>
</table>
</div>

Pour utiliser un des plugins exemples au-dessus comme illustration, voici comment vous devriez spécifier ces deux flags :

{% highlight ruby %}
module Jekyll
  class UpcaseConverter < Converter
    safe true
    priority :low
    ...
  end
end
{% endhighlight %}

## Plugins Disponibles

Vous pouvez trouver quelques plugings utiles aux endroits suivants : 

#### Générateurs

- [ArchiveGenerator by Ilkka Laukkanen](https://gist.github.com/707909) : Utilisez [cette page archive](https://gist.github.com/707020) pour générer des archives.
- [LESS.js Generator by Andy Fowler](https://gist.github.com/642739) : Renders LESS.js files during generation.
- [Version Reporter by Blake Smith](https://gist.github.com/449491) : Creates a version.html file containing the Jekyll version.
- [Sitemap.xml Generator by Michael Levin](https://github.com/kinnetica/jekyll-plugins) : Generates a sitemap.xml file by traversing all of the available posts and pages.
- [Full-text search by Pascal Widdershoven](https://github.com/PascalW/jekyll_indextank) : Ajoute une recherche plein-texte à votre site Jekyll avec un plugin et un peu de JavaScript.
- [AliasGenerator by Thomas Mango](https://github.com/tsmango/jekyll_alias_generator) : Generates redirect pages for posts when an alias is specified in the YAML Front Matter.
- [Pageless Redirect Generator by Nick Quinlan](https://github.com/nquinlan/jekyll-pageless-redirects): Generates redirects based on files in the Jekyll root, with support for htaccess style redirects.
- [Projectlist by Frederic Hemberger](https://github.com/fhemberger/jekyll-projectlist): Renders files in a directory as a single page instead of separate posts.
- [RssGenerator by Assaf Gelber](https://github.com/agelber/jekyll-rss): Automatically creates an RSS 2.0 feed from your posts.
- [Monthly archive generator by Shigeya Suzuki](https://github.com/shigeya/jekyll-monthly-archive-plugin): Generator and template which renders monthly archive like MovableType style, based on the work by Ilkka Laukkanen and others above.
- [Category archive generator by Shigeya Suzuki](https://github.com/shigeya/jekyll-category-archive-plugin): Generator and template which renders category archive like MovableType style, based on Monthly archive generator.
- [Emoji for Jekyll](https://github.com/yihangho/emoji-for-jekyll): Seamlessly enable emoji for all posts and pages.

#### Convertisseurs

- [Jade plugin by John Papandriopoulos](https://github.com/snappylabs/jade-jekyll-plugin): Jade converter for Jekyll.
- [HAML plugin by Sam Z](https://gist.github.com/517556): HAML converter for Jekyll.
- [HAML-Sass Converter by Adam Pearson](https://gist.github.com/481456): Simple HAML-Sass converter for Jekyll. [Fork](https://gist.github.com/528642) by Sam X.
- [Sass SCSS Converter by Mark Wolfe](https://gist.github.com/960150): Sass converter which uses the new CSS compatible syntax, based Sam X’s fork above.
- [LESS Converter by Jason Graham](https://gist.github.com/639920): Convert LESS files to CSS.
- [LESS Converter by Josh Brown](https://gist.github.com/760265): Simple LESS converter.
- [Upcase Converter by Blake Smith](https://gist.github.com/449463): An example Jekyll converter.
- [CoffeeScript Converter by phaer](https://gist.github.com/959938): A [CoffeeScript](http://coffeescript.org) to Javascript converter.
- [Markdown References by Olov Lassus](https://github.com/olov/jekyll-references): Keep all your markdown reference-style link definitions in one \_references.md file.
- [Stylus Converter](https://gist.github.com/988201): Convert .styl to .css.
- [ReStructuredText Converter](https://github.com/xdissent/jekyll-rst): Converts ReST documents to HTML with Pygments syntax highlighting.
- [Jekyll-pandoc-plugin](https://github.com/dsanson/jekyll-pandoc-plugin): Use pandoc for rendering markdown.
- [Jekyll-pandoc-multiple-formats](https://github.com/fauno/jekyll-pandoc-multiple-formats) by [edsl](https://github.com/edsl): Use pandoc to generate your site in multiple formats. Supports pandoc’s markdown extensions.
- [ReStructuredText Converter](https://github.com/xdissent/jekyll-rst): Converts ReST documents to HTML with Pygments syntax highlighting.
- [Transform Layouts](https://gist.github.com/1472645): Allows HAML layouts (you need a HAML Converter plugin for this to work).
- [Org-mode Converter](https://gist.github.com/abhiyerra/7377603): Org-mode converter for Jekyll.

#### Filtres

- [Truncate HTML](https://github.com/MattHall/truncatehtml) by [Matt Hall](http://codebeef.com): A Jekyll filter that truncates HTML while preserving markup structure.
- [Domain Name Filter by Lawrence Woodman](https://github.com/LawrenceWoodman/domain_name-liquid_filter): Filters the input text so that just the domain name is left.
- [Summarize Filter by Mathieu Arnold](https://gist.github.com/731597): Remove markup after a `<div id="extended">` tag.
- [URL encoding by James An](https://gist.github.com/919275): Percent encoding for URIs.
- [JSON Filter](https://gist.github.com/1850654) by [joelverhagen](https://github.com/joelverhagen): Filter that takes input text and outputs it as JSON. Great for rendering JavaScript.
- [i18n_filter](https://github.com/gacha/gacha.id.lv/blob/master/_plugins/i18n_filter.rb): Liquid filter to use I18n localization.
- [Smilify](https://github.com/SaswatPadhi/jekyll_smilify) by [SaswatPadhi](https://github.com/SaswatPadhi): Convert text emoticons in your content to themeable smiley pics ([Demo](http://saswatpadhi.github.com/)).
- [Read in X Minutes](https://gist.github.com/zachleat/5792681) by [zachleat](https://github.com/zachleat): Estimates the reading time of a string (for blog post content).
- [Jekyll-timeago](https://github.com/markets/jekyll-timeago): Converts a time value to the time ago in words.
- [pluralize](https://github.com/bdesham/pluralize): Easily combine a number and a word into a gramatically-correct amount like “1 minute” or “2 minute**s**”.
- [reading_time](https://github.com/bdesham/reading_time): Count words and estimate reading time for a piece of text, ignoring HTML elements that are unlikely to contain running text.
- [Table of Content Generator](https://github.com/dafi/jekyll-toc-generator): Generate the HTML code containing a table of content (TOC), the TOC can be customized in many way, for example you can decide which pages can be without TOC.

#### Tags

- [Asset Path Tag](https://github.com/samrayner/jekyll-asset-path-plugin) by [Sam Rayner](http://www.samrayner.com/): Allows organisation of assets into subdirectories by outputting a path for a given file relative to the current post or page.
- [Delicious Plugin by Christian Hellsten](https://github.com/christianhellsten/jekyll-plugins): Fetches and renders bookmarks from delicious.com.
- [Ultraviolet Plugin by Steve Alex](https://gist.github.com/480380): Jekyll tag for the [Ultraviolet](http://ultraviolet.rubyforge.org/) code highligher.
- [Tag Cloud Plugin by Ilkka Laukkanen](https://gist.github.com/710577): Generate a tag cloud that links to tag pages.
- [GIT Tag by Alexandre Girard](https://gist.github.com/730347): Add Git activity inside a list.
- [MathJax Liquid Tags by Jessy Cowan-Sharp](https://gist.github.com/834610): Simple liquid tags for Jekyll that convert inline math and block equations to the appropriate MathJax script tags.
- [Non-JS Gist Tag by Brandon Tilley](https://gist.github.com/1027674) A Liquid tag that embeds Gists and shows code for non-JavaScript enabled browsers and readers.
- [Render Time Tag by Blake Smith](https://gist.github.com/449509): Displays the time a Jekyll page was generated.
- [Status.net/OStatus Tag by phaer](https://gist.github.com/912466): Displays the notices in a given status.net/ostatus feed.
- [Raw Tag by phaer](https://gist.github.com/1020852): Keeps liquid from parsing text betweeen `raw` tags.
- [Embed.ly client by Robert Böhnke](https://github.com/robb/jekyll-embedly-client): Autogenerate embeds from URLs using oEmbed.
- [Logarithmic Tag Cloud](https://gist.github.com/2290195): Flexible. Logarithmic distribution. Documentation inline.
- [oEmbed Tag by Tammo van Lessen](https://gist.github.com/1455726): Enables easy content embedding (e.g. from YouTube, Flickr, Slideshare) via oEmbed.
- [FlickrSetTag by Thomas Mango](https://github.com/tsmango/jekyll_flickr_set_tag): Generates image galleries from Flickr sets.
- [Tweet Tag by Scott W. Bradley](https://github.com/scottwb/jekyll-tweet-tag): Liquid tag for [Embedded Tweets](https://dev.twitter.com/docs/embedded-tweets) using Twitter’s shortcodes.
- [Jekyll-contentblocks](https://github.com/rustygeldmacher/jekyll-contentblocks): Lets you use Rails-like content_for tags in your templates, for passing content from your posts up to your layouts.
- [Generate YouTube Embed](https://gist.github.com/1805814) by [joelverhagen](https://github.com/joelverhagen): Jekyll plugin which allows you to embed a YouTube video in your page with the YouTube ID. Optionally specify width and height dimensions. Like “oEmbed Tag” but just for YouTube.
- [Jekyll-beastiepress](https://github.com/okeeblow/jekyll-beastiepress): FreeBSD utility tags for Jekyll sites.
- [Jsonball](https://gist.github.com/1895282): Reads json files and produces maps for use in Jekyll files.
- [Bibjekyll](https://github.com/pablooliveira/bibjekyll): Render BibTeX-formatted bibliographies/citations included in posts and pages using bibtex2html.
- [Jekyll-citation](https://github.com/archome/jekyll-citation): Render BibTeX-formatted bibliographies/citations included in posts and pages (pure Ruby).
- [Jekyll Dribbble Set Tag](https://github.com/ericdfields/Jekyll-Dribbble-Set-Tag): Builds Dribbble image galleries from any user.
- [Debbugs](https://gist.github.com/2218470): Allows posting links to Debian BTS easily.
- [Refheap_tag](https://github.com/aburdette/refheap_tag): Liquid tag that allows embedding pastes from [refheap](https://refheap.com).
- [Jekyll-devonly_tag](https://gist.github.com/2403522): A block tag for including markup only during development.
- [JekyllGalleryTag](https://github.com/redwallhp/JekyllGalleryTag) by [redwallhp](https://github.com/redwallhp): Generates thumbnails from a directory of images and displays them in a grid.
- [Youku and Tudou Embed](https://gist.github.com/Yexiaoxing/5891929): Liquid plugin for embedding Youku and Tudou videos.
- [Jekyll-swfobject](https://github.com/sectore/jekyll-swfobject): Liquid plugin for embedding Adobe Flash files (.swf) using [SWFObject](http://code.google.com/p/swfobject/).
- [Jekyll Picture Tag](https://github.com/robwierzbowski/jekyll-picture-tag): Easy responsive images for Jekyll. Based on the proposed [`<picture>`](http://picture.responsiveimages.org/) element, polyfilled with Scott Jehl’s [Picturefill](https://github.com/scottjehl/picturefill).
- [Jekyll Image Tag](https://github.com/robwierzbowski/jekyll-image-tag): Better images for Jekyll. Save image presets, generate resized images, and add classes, alt text, and other attributes.
- [Ditaa Tag](https://github.com/matze/jekyll-ditaa) by [matze](https://github.com/matze): Renders ASCII diagram art into PNG images and inserts a figure tag.
- [Good Include](https://github.com/penibelst/jekyll-good-include) by [Anatol Broder](http://penibelst.de/): Strips newlines and whitespaces from the end of include files before processing.
- [Jekyll Suggested Tweet](https://github.com/davidensinger/jekyll-suggested-tweet) by [David Ensinger](https://github.com/davidensinger/): A Liquid tag for Jekyll that allows for the embedding of suggested tweets via Twitter’s Web Intents API.
- [Jekyll Date Chart](https://github.com/GSI/jekyll_date_chart) by [GSI](https://github.com/GSI): Block that renders date line charts based on textile-formatted tables.
- [Jekyll Image Encode](https://github.com/GSI/jekyll_image_encode) by [GSI](https://github.com/GSI): Tag that renders base64 codes of images fetched from the web.
- [Jekyll Quick Man](https://github.com/GSI/jekyll_quick_man) by [GSI](https://github.com/GSI): Tag that renders pretty links to man page sources on the internet.

#### Collections

- [Jekyll Plugins by Recursive Design](http://recursive-design.com/projects/jekyll-plugins/): Plugins to generate Project pages from GitHub readmes, a Category page, and a Sitemap generator.
- [Company website and blog plugins](https://github.com/flatterline/jekyll-plugins) by Flatterline, a [Ruby on Rails development company](http://flatterline.com/): Portfolio/project page generator, team/individual page generator, an author bio liquid tag for use on posts, and a few other smaller plugins.
- [Jekyll plugins by Aucor](https://github.com/aucor/jekyll-plugins): Plugins for trimming unwanted newlines/whitespace and sorting pages by weight attribute.

#### Autres

- [Pygments Cache Path by Raimonds Simanovskis](https://github.com/rsim/blog.rayapps.com/blob/master/_plugins/pygments_cache_patch.rb): Plugin to cache syntax-highlighted code from Pygments.
- [Draft/Publish Plugin by Michael Ivey](https://gist.github.com/49630): Save posts as drafts.
- [Growl Notification Generator by Tate Johnson](https://gist.github.com/490101): Send Jekyll notifications to Growl.
- [Growl Notification Hook by Tate Johnson](https://gist.github.com/525267): Better alternative to the above, but requires his “hook” fork.
- [Related Posts by Lawrence Woodman](https://github.com/LawrenceWoodman/related_posts-jekyll_plugin): Overrides `site.related_posts` to use categories to assess relationship.
- [Tiered Archives by Eli Naeher](https://gist.github.com/88cda643aa7e3b0ca1e5): Create tiered template variable that allows you to group archives by year and month.
- [Jekyll-localization](https://github.com/blackwinter/jekyll-localization): Jekyll plugin that adds localization features to the rendering engine.
- [Jekyll-rendering](https://github.com/blackwinter/jekyll-rendering): Jekyll plugin to provide alternative rendering engines.
- [Jekyll-pagination](https://github.com/blackwinter/jekyll-pagination): Jekyll plugin to extend the pagination generator.
- [Jekyll-tagging](https://github.com/pattex/jekyll-tagging): Jekyll plugin to automatically generate a tag cloud and tag pages.
- [Jekyll-scholar](https://github.com/inukshuk/jekyll-scholar): Jekyll extensions for the blogging scholar.
- [Jekyll-asset_bundler](https://github.com/moshen/jekyll-asset_bundler): Bundles and minifies JavaScript and CSS.
- [Jekyll-assets](http://ixti.net/jekyll-assets/) by [ixti](https://github.com/ixti): Rails-alike assets pipeline (write assets in CoffeeScript, Sass, LESS etc; specify dependencies for automatic bundling using simple declarative comments in assets; minify and compress; use JST templates; cache bust; and many-many more).
- [File compressor](https://gist.github.com/2758691) by [mytharcher](https://github.com/mytharcher): Compress HTML and JavaScript files on site build.
- [Jekyll-minibundle](https://github.com/tkareine/jekyll-minibundle): Asset bundling and cache busting using external minification tool of your choice. No gem dependencies.
- [Singlepage-jekyll](https://github.com/JCB-K/singlepage-jekyll) by [JCB-K](https://github.com/JCB-K): Turns Jekyll into a dynamic one-page website.
- [generator-jekyllrb](https://github.com/robwierzbowski/generator-jekyllrb): A generator that wraps Jekyll in [Yeoman](http://yeoman.io/), a tool collection and workflow for builing modern web apps.
- [grunt-jekyll](https://github.com/dannygarcia/grunt-jekyll): A straightforward [Grunt](http://gruntjs.com/) plugin for Jekyll.
- [jekyll-postfiles](https://github.com/indirect/jekyll-postfiles): Add `_postfiles` directory and {% raw %}`{{ postfile }}`{% endraw %} tag so the files a post refers to will always be right there inside your repo.

<div class="note info">
  <h5>Plugins Jekyll Voulus</h5>
  <p>
    Si vous avez un plugin Jekyll que vous aimeriez voir ajouté à cette liste, vous devriez 
    <a href="../contributing/">lire la page contribution</a> pour voir comment faire ça.
  </p>
</div>
