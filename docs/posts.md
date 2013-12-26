---
layout: docs
title: Écrire des posts
prev_section: frontmatter
next_section: drafts
permalink: /docs/posts/
---

L'un des aspects les plus intéressants de Jekyll est qu'il est “conscient des blogs”. Qu'est-ce que ça veut dire plus précisément ? Dit plus simplement, cela signifie que le blogging est intégré dans les fonctionnalités de Jekyll. Si vous écrivez des articles et les publiez en ligne, ceci signifie que vous pouvez publier et maintenir simplement un blog en gérant un répertoire ou des fichiers-texte sur votre ordinateur. Si vous comparez cela à tous les tracas de configuration et de maintenance des bases de données et des systèmes de gestion de contenus basés sur le web, ceci sera un changement bienvenu.

## Le Répertoire Posts

Comme cela est expliqué sur la page [Structure des Répertoires](../structure/), le répertoire `_posts` est l'endroit où vivront vos posts de blog. Ces fichiers peuvent être soit formatés sous forme de fichiers texte [Markdown](http://daringfireball.net/projects/markdown/) ou [Textile](http://textile.sitemonks.com/), et tant qu'ils ont un [front-matter YAML](../frontmatter/), ils seront convertis à partir du format source à l'intérieur d'une page HTML qui fera partie de votre site statique.

### Créer des Fichiers Post

Pour créer un nouveau post, tout ce que vous devez faire c'est créer un nouveau fichier dans le répertoire `_posts`. Le nom que vous allez donner à ces fichiers dans ce répertoire est important. Jekyll requiert que les fichiers des posts de blog soient nommées selon le format suivant : 

{% highlight bash %}
ANNEE-MOIS-JOUR-title.MARKUP
{% endhighlight %}

Où `ANNEE` est un nombre à quatre chiffres, `MOIS` et `JOUR` sont tous deux des nombres à deux chiffres, et `MARKUP` est l'extension-fichier représentant le format utilisé pour le fichier. Par exemple, les exemples qui suivent sont des noms de fichiers de post valides : 

{% highlight bash %}
2013-12-31-la-nouvelle-annee-est-merveilleuse.md
2013-09-12-comment-ecrire-un-billet-de-blog.textile
{% endhighlight %}

### Formats de Contenu

Tous les fichiers de post de blog commencent par un [front- matter YAML](../frontmatter/). Après ça, la seule question à vous poser est de décider du format que vous préférez. Jekyll supporte deux formats de contenu très connus : [Markdown](http://daringfireball.net/projects/markdown/) et [Textile](http://textile.sitemonks.com/). Ces formats ont chacun leurs  façons particulières de marquer différents types de contenus dans un post. Par conséquent, vous devriez vous familiariser avec ces formats puis décider lequel correspond le mieux à vos besoins.

## Inclure des images et ressources

Il est plus que probable qu'une fois parvenu à un certain niveau, vous ayez envie d'ajouter des images, téléchargements, ou tout autre actif digital pouvant cohabiter avec votre contenu texte. Même si la syntaxe pour lier vers ces ressources diffère entre Markdown et Textile, le problème de trouver l'endroit où stocker ces fichiers est quelque chose que tout le monde rencontrera.

Du fait de la flexibilité de Jekyll, il existe tout un tas de solutions pour faire ça. Une solution commune est de créer un dossier dans la racine du répertoire projet appelé parfois `assets` ou `downloads`, à l'intérieur duquel seront placés toutes les images, téléchargements ou autres ressources. Ensuite, à partir de l'intérieur de n'importe quel post, ils peuvent être liés en utilisant la racine du site comme chemin pour l'actif à inclure. De nouveau, ceci dépendra de la manière dont le (sous)domaine et le chemin de votre site sont configurés, mais voici quelques exemples (en Markdown) sur la façon de faire ça en utilisant la variable `site.url` dans un post.

Inclure un objet image dans un post : 

{% highlight text %}
… qui est montré dans l'écran en-dessous:
![Mon screenshot d'aide]({% raw %}{{ site.url }}{% endraw %}/assets/screenshot.jpg)
{% endhighlight %}

Faire un lien vers un PDF offert en téléchargement :

{% highlight text %}
… vous pouvez [télécharger le PDF]({% raw %}{{ site.url }}{% endraw %}/assets/mydoc.pdf) directement.
{% endhighlight %}

<div class="note">
  <h5>ProTruc™ : Lier en utilisant simplement l'URL racine du site</h5>
  <p>
    Vous pouvez ôter la variable <code>{% raw %}{{ site.url }}{% endraw %}</code> 
    si vous <strong>savez</strong> que votre site sera toujours affiché sur l'URL racine de votre domaine. Dans ce cas vous pouvez référencer les actifs directement avec simplement le <code>/path/file.jpg</code>.
  </p>
</div>

## Afficher un index des posts

C'est très bien d'avoir des posts dans un répertoire, mais un blog ne sert à rien si vous ne disposez pas quelque part d'une liste des posts. Créer un index de posts sur une autre page 
(ou dans un [template](../templates/)) est facile, grâce au [langage de template Liquid](http://wiki.shopify.com/Liquid) et ses tags. Voici un exemple basique pour créer une liste de liens vers vos posts de blog : 

{% highlight html %}
<ul>
  {% raw %}{% for post in site.posts %}{% endraw %}
    <li>
      <a href="{% raw %}{{ post.url }}{% endraw %}">{% raw %}{{ post.title }}{% endraw %}</a>
    </li>
  {% raw %}{% endfor %}{% endraw %}
</ul>
{% endhighlight %}

Bien sûr, vous avez une maîtrise complète sur la façon (et où) de présenter vos posts, et comment vous structurez votre site. Pour en savoir plus, vous devriez lire [comment fonctionnent les templates](../templates/) avec Jekyll.

## Extraits de Post

Chaque post prend automatiquement le premier bloc de texte, à partir du début du contenu jusqu'à la première occurrence de `excerpt_separator`, et le règle comme le `post.excerpt`.
Prenez l'exemple du-dessus d'un index de posts. Peut-être que vous voulez inclure un petit truc concernant le contenu du post en ajoutant le premier paragraphe de vos posts : 

{% highlight html %}
<ul>
  {% raw %}{% for post in site.posts %}{% endraw %}
    <li>
      <a href="{% raw %}{{ post.url }}{% endraw %}">{% raw %}{{ post.title }}{% endraw %}</a>
      <p>{% raw %}{{ post.excerpt }}{% endraw %}</p>
    </li>
  {% raw %}{% endfor %}{% endraw %}
</ul>
{% endhighlight %}

Si vous n'aimez pas l'extrait de post automatiquement généré, il peut être écrasé en ajoutant 
`excerpt` au front-matter YAML de votre post. Vous pouvez le désactiver complètement en réglant votre `excerpt_separator` sur `""`.

## Coloration syntaxique des fragments de code 

Jekyll a aussi un support intégré pour la coloration syntaxique des fragments de code en utilisant Pygments, et inclure un fragment de code dans n'importe quel post est facile. Utilisez simplement le tag dédié Liquid comme suit : 

{% highlight text %}
{% raw %}{% highlight ruby %}{% endraw %}
def show
  @widget = Widget(params[:id])
  respond_to do |format|
    format.html # show.html.erb
    format.json { render json: @widget }
  end
end
{% raw %}{% endhighlight %}{% endraw %}
{% endhighlight %}

Et le rendu s'affichera comme ça : 

{% highlight ruby %}
def show
  @widget = Widget(params[:id])
  respond_to do |format|
    format.html # show.html.erb
    format.json { render json: @widget }
  end
end
{% endhighlight %}

<div class="note">
  <h5>ProTruc™ : Afficher les numéros de ligne</h5>
  <p>
    Vous pouvez produire des fragments de code en incluant des numéros de ligne en ajoutant le mot  <code>linenos</code> à la fin du tag d'ouverture de coloration syntaxique code comme ceci : 
    <code>{% raw %}{% highlight ruby linenos %}{% endraw %}</code>.
  </p>
</div>

Ces fondamentaux devraient vous suffire pour écrire vos premiers posts. Quand vous serez prêts pour plonger dans tout ce qu'il est possible de faire, vous pourriez être intéressé par des trucs comme la possibilité de[personnaliser les permaliens des posts](../permalinks/) ou d'utiliser des [variables personnalisées](../variables/) dans vos posts et n'importe où sur votre site.
