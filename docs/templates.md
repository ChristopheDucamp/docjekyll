---
layout: docs
title: Templates
prev_section: migrations
next_section: permalinks
permalink: /docs/templates/
---

Jekyll utilise le langage de template [Liquid](http://wiki.shopify.com/Liquid) pour traiter les templates. Tous les [tags](http://wiki.shopify.com/Logic) et les [filtres](http://wiki.shopify.com/Filters) standards Liquid sont supportés. Jekyll ajoute en plus quelques filtres et tags pratiques pour faciliter des tâches communes.

## Filtres

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>Description</th>
      <th><span class="filter">Filtre</span> et <span class="output">Output</span></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p class='name'><strong>Date to XML Schema</strong></p>
        <p>Convertit une Date au format Schéma XML (ISO 8601).</p>
      </td>
      <td class='align-center'>
        <p>
         <code class='filter'>{% raw %}{{ site.time | date_to_xmlschema }}{% endraw %}</code>
        </p>
        <p>
          <code class='output'>2008-11-07T13:07:54-08:00</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class='name'><strong>Date to RFC-822</strong></p>
        <p>Convertit une Date dans le format RFC-822 utilisé pour les flux RSS.</p>
      </td>
      <td class='align-center'>
        <p>
         <code class='filter'>{% raw %}{{ site.time | date_to_rfc822 }}{% endraw %}</code>
        </p>
        <p>
          <code class='output'>Mon, 07 Nov 2008 13:07:54 -0800</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class='name'><strong>Date to String</strong></p>
        <p>Convertit une date pour raccourcir le format.</p>
      </td>
      <td class='align-center'>
        <p>
         <code class='filter'>{% raw %}{{ site.time | date_to_string }}{% endraw %}</code>
        </p>
        <p>
          <code class='output'>07 Nov 2008</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class='name'><strong>Date to Long String</strong></p>
        <p>Formate une date dans un format long.</p>
      </td>
      <td class='align-center'>
        <p>
         <code class='filter'>{% raw %}{{ site.time | date_to_long_string }}{% endraw %}</code>
        </p>
        <p>
          <code class='output'>07 November 2008</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class='name'><strong>XML Escape</strong></p>
        <p>Escape quelque texte pour usage en XML.</p>
      </td>
      <td class='align-center'>
        <p>
         <code class='filter'>{% raw %}{{ page.content | xml_escape }}{% endraw %}</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class='name'><strong>CGI Escape</strong></p>
        <p>
          CGI escape une chaîne à utiliser dans une URL. Remplace tous les caractères spéciaux
          avec les remplacements %XX appropriés.
        </p>
      </td>
      <td class='align-center'>
        <p>
         <code class='filter'>{% raw %}{{ “foo,bar;baz?” | cgi_escape }}{% endraw %}</code>
        </p>
        <p>
          <code class='output'>foo%2Cbar%3Bbaz%3F</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class='name'><strong>URI Escape</strong></p>
        <p>
          URI escape a string.
        </p>
      </td>
      <td class='align-center'>
        <p>
         <code class='filter'>{% raw %}{{ “'foo, bar \\baz?'” | uri_escape }}{% endraw %}</code>
        </p>
        <p>
          <code class='output'>foo,%20bar%20%5Cbaz?</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class='name'><strong>number_of_words</strong></p>
        <p>Compte le nombre de mots dans n'importe quel texte.</p>
      </td>
      <td class='align-center'>
        <p>
         <code class='filter'>{% raw %}{{ page.content | number_of_words }}{% endraw %}</code>
        </p>
        <p>
          <code class='output'>1337</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class='name'><strong>Array to Sentence</strong></p>
        <p>Convert an array into a sentence. Useful for listing tags.</p>
      </td>
      <td class='align-center'>
        <p>
         <code class='filter'>{% raw %}{{ page.tags | array_to_sentence_string }}{% endraw %}</code>
        </p>
        <p>
          <code class='output'>foo, bar, and baz</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class='name'><strong>Textilize</strong></p>
        <p>Convertit une chaîne formatée-Textile en HTML, formaté via RedCloth</p>
      </td>
      <td class='align-center'>
        <p>
         <code class='filter'>{% raw %}{{ page.excerpt | textilize }}{% endraw %}</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class='name'><strong>Markdownify</strong></p>
        <p>Convertit une chaîne formaté-Markdown en HTML.</p>
      </td>
      <td class='align-center'>
        <p>
         <code class='filter'>{% raw %}{{ page.excerpt | markdownify }}{% endraw %}</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p class='name'><strong>Data To JSON</strong></p>
        <p>Convertit les Hash ou Array vers JSON.</p>
      </td>
      <td class='align-center'>
        <p>
         <code class='filter'>{% raw %}{{ site.data.projects | jsonify }}{% endraw %}</code>
        </p>
      </td>
    </tr>
  </tbody>
</table>
</div>

## Tags

### Includes

Si vous avez des petits fragments de page que vous souhaitez inclure à plusieurs endroits sur votre site, vous pouvez utiliser le tag `include`.

{% highlight ruby %}
{% raw %}{% include footer.html %}{% endraw %}
{% endhighlight %}

Jekyll s'attend à ce que tous les fichiers include soient placés dans un répertoire `_includes` à la racine de votre répertoire source. Ceci embarquera les contenus du `<source>/_includes/footer.html` à l'intérieur du fichier appelé.

<div class="note">
  <h5>ProTruc™ : Utilisez les variables comme un nom de fichier</h5>
  <p>

    Le nom de fichier que vous souhaitez embarquer peut être littéral (comme dans l'exemple au-dessus), 
    ou vous pouvez utiliser une variable, en utilisant une syntaxe variable de type-Liquid comme dans 
    <code>{% raw %}{% include {{ ma_variable }} %}{% endraw %}</code>.
   </p>
</div>

Vous pouvez aussi les paramètres vers un include :

{% highlight ruby %}
{% raw %}{% include footer.html param="value" %}{% endraw %}
{% endhighlight %}

Ces paramètres sont disponibles via Liquid dans l'include : 

{% highlight ruby %}
{% raw %}{{ include.param }}{% endraw %}
{% endhighlight %}

### Coloration Syntaxique de fragment de code

Jekyll a un support intégré pour la coloration syntaxique sur [plus de 100
langages](http://pygments.org/languages/) grâce à [Pygments](http://pygments.org/). Pour utiliser Pygments, vous devez avoir installé Python sur votre système et régler `pygments` sur `true` dans le fichier de configuration de votre site.

Pour afficher un bloc de code avec une coloration syntaxique, entourez votre cotre code comme suit : 

{% highlight text %}
{% raw %}
{% highlight ruby %}
def foo
  puts 'foo'
end
{% endhighlight %}
{% endraw %}
{% endhighlight %}

L'argument vers le tag `highlight` (`ruby` dans l'exemple au-dessus) est l'identifiant du langage. 
Pour trouver l'identifiant adéquat à utiliser pour le langage que vous voulez colorer, regardez son raccourci -le “short name”- sur la [page Lexers](http://pygments.org/docs/lexers/).

#### Numéros de ligne

Il existe un second argument à `highlight` appelé `linenos` qui est optionnel.
Inclure l'argument `linenos` forcera le code coloré à inclure les numéros de ligne. Par exemple, le bloc de code suivant inclura des numéros de ligne à côté de chaque ligne :

{% highlight text %}
{% raw %}
{% highlight ruby linenos %}
def foo
  puts 'foo'
end
{% endhighlight %}
{% endraw %}
{% endhighlight %}

#### Feuiles de Style pour la coloration syntaxique

Afin que la coloration s'affiche, vous devrez inclure une feuille de style de mise en valeur. Pour un exemple de feuille de style, vous pouvez regarder [syntax.css](http://github.com/mojombo/tpw/tree/master/css/syntax.css). Ce sont les mêmes styles que ceux utilisés par GitHub et vous êtes libres de les utiliser pour votre propre site. Si vous utilisez `linenos`, vous pourriez vouloir inclure une définition de classe supplémentaire CSS pour la classe  `.lineno` dans `syntax.css` afin de distinguer les numéros de ligne provenant du code mis en valeur.

### URL de Post

Si vous voulez inclure un lien à l'intérieur d'un post sur votre site, le tag `post_url` générera le permalien URL correct pour le post que vous spécifiez.

{% highlight text %}
{% raw %}
{% post_url 2010-07-06-nom-du-post %}
{% endraw %}
{% endhighlight %}

Si vous organisez vos posts dans des sous-répertoires, vous devrez inclure un chemin de sous-répertoire vers le post : 

{% highlight text %}
{% raw %}
{% post_url /subdir/2010-07-21-nom-du-post %}
{% endraw %}
{% endhighlight %}

Il n'y aura pas besoin d'inclure l'extension de fichier au moment d'utiliser le tag `post_url`.

Vous pouvez aussi utiliser ce tag pour créer un lien vers un post en Markdown comme suit  :

{% highlight text %}
{% raw %}
[Nom du Lien]({% post_url 2010-07-06-nom-du-post %})
{% endraw %}
{% endhighlight %}

### Gist

Utilisez le tag `gist` pour embarquer facilement un Gist GitHub Gist sur votre site : 

{% highlight text %}
{% raw %}
{% gist 5555251 %}
{% endraw %}
{% endhighlight %}

Vous pouvez spécifier optionnellement le nom de fichier dans le gist à afficher : 

{% highlight text %}
{% raw %}
{% gist 5555251 result.md %}
{% endraw %}
{% endhighlight %}

Le tag `gist` fonctionne aussi avec des gists privés, qui requièrent le nom d'utilisateur github du propriétaire du gist :

{% highlight text %}
{% raw %}
{% gist parkr/931c1c8d465a04042403 %}
{% endraw %}
{% endhighlight %}

La syntaxe pour le gist privé supporte aussi les noms de fichiers.
