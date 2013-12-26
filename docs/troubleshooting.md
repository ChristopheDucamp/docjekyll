---
layout: docs
title: Dépannage
prev_section: deployment-methods
next_section: sites
permalink: /docs/troubleshooting/
---

Si vous avez déjà rencontré quelques problèmes pour installer ou utiliser Jekyll, voici quelques petits trucs qui pourront vous aider. 
Si le problème que vous rencontrez n'est pas couvert en-dessous, SVP [rendez compte du problème]({{ site.repository }}/issues/new) afin que la communauté puisse améliorer l'expérience de tous.

## Problèmes d'Installation

Si vous rencontrez des erreurs durant l'installation de gem, vous pourriez avoir besoin d'installer les fichiers header pour les modules de compilation d'extension pour ruby 1.9.1. Ceci peut être fait sur 
Ubuntu ou Debian en faisant tourner :

{% highlight bash %}
sudo apt-get install ruby1.9.1-dev
{% endhighlight %}

Sur les systèmes Red Hat, CentOS et Fedora vous pouvez faire ça en faisant tourner :

{% highlight bash %}
sudo yum install ruby-devel
{% endhighlight %}

Sur [NearlyFreeSpeech](http://nearlyfreespeech.net/) vous devez lancer la commande avec la variable d'environnement suivante : 

{% highlight bash %}
RB_USER_INSTALL=true gem install jekyll
{% endhighlight %}

Sur OSX, vous pourriez devoir mettre à jour RubyGems :

{% highlight bash %}
sudo gem update --system
{% endhighlight %}

Si vous avez encore des problèmes, vous pourriez avoir besoin d'[utiliser les Outils de Ligne de Commande XCode](http://www.zlu.me/blog/2012/02/21/install-native-ruby-gem-in-mountain-lion-preview/)
qui vous permettront d'installer les gems natives en utilisant la commande suivante : 

{% highlight bash %}
sudo gem install jekyll
{% endhighlight %}

Pour installer RubyGems sur Gentoo :

{% highlight bash %}
sudo emerge -av dev-ruby/rubygems
{% endhighlight %}

Sur Windows, vous pourriez avoir besoin d'installer [RubyInstaller
DevKit](http://wiki.github.com/oneclick/rubyinstaller/development-kit).

## Problèmes de fonctionnement Jekyll

Sur Debian ou Ubuntu, vous pourriez avoir besoin d'ajouter `/var/lib/gems/1.8/bin/` à votre chemin afin que l'exécutable `jekyll` soit disponible dans votre Terminal.

## Problèmes de Base-URL

Si vous utilisez une option base-url option comme :

{% highlight bash %}
jekyll serve --baseurl '/blog'
{% endhighlight %}

… assurez-vous ensuite que vous avez accès au site sur : 

{% highlight bash %}
http://localhost:4000/blog/index.html
{% endhighlight %}

Cela ne fonctionnera pas pour accéder simplement à 

{% highlight bash %}
http://localhost:4000/blog
{% endhighlight %}

## Problèmes de configuration 

L'ordre de précédence des conflits pour les [réglages de configuration](../configuration/)  se fait comme suit : 


1.  Flags ligne-de-commande
2.  Réglages fichier de configuration
3.  Défauts

Ce qui veut dire : les valeurs par défaut sont écrasées par les options dans `_config.yml`, et les flags spécifiés à la ligne de commande écraseront tous les autres paramétrages spécifiés ailleurs.

## Problèmes de Marquage

Les différents moteurs de marquage que Jekyll utilise peuvent avoir quelques problèmes. Cette page les documentera afin d'aider les autres qui pourront rencontrer les mêmes problèmes.

### Maruku

Si votre lien a des caractères qui doivent être échappés, vous devez utiliser cette syntaxe : 

{% highlight text %}
![Texte alt](http://yuml.me/diagram/class/[Projet]->[Tache])
{% endhighlight %}

Si vous avez un tag vide, par ex. `<script src="js.js"></script>`, Maruku transforme ça en `<script src="js.js" />`. Ceci provoque des problèmes dans Firefox et probablement d'autres navigateurs et c'est [déconseillé en XHTML.](http://www.w3.org/TR/xhtml1/#C_3). 
Une réparation facile est de placer un espace entre les balises d'ouverture et de fermeture.

### RedCloth

Les versions 4.1.1 et suivantes n'obéissent pas à la balise notextile. [C'est un bug connu](http://aaronqian.com/articles/2009/04/07/redcloth-ate-my-notextile.html) et qui, nous l'espérons, sera résolu pour la 4.2. Vous pouvez encore utiliser la 4.1.9, mais la suite de test requiert que 4.1.0 soit installée. Si vous utilisez une version de RedCloth qui n'a pas la balise notextile, vous pouvez remarquer que les blocs de syntaxe mis en valeur à partir de Pygments ne sont pas mis en page correctement, parmi d'autres choses. Si vous voyez ceci, installez simplement 4.1.0.

### Liquid

La toute dernière version, la version 2.0, semble briser l'usage de `{{ "{{" }}` dans les templates. À la différence des versions précédentes, utilisant `{{ "{{" }}` dans 2.0 déclenche l'erreur suivante : 

{% highlight bash %}
'{{ "{{" }}' was not properly terminated with regexp: /\}\}/  (Liquid::SyntaxError)
{% endhighlight %}

### Extraits

Depuis la v1.0.0, Jekyll dispose d'extraits de posts automatiquement-générés. Depuis la v1.1.0, Jekyll passe aussi ces extraits à travers Liquid, ce qui peut provoquer des erreurs étranges où les références 
n'existent pas ou une balise n'a pas été fermée. Si vous rencontrez ces erreurs, essayez de réglér `excerpt_separator: ""` dans votre fichier 
`_config.yml`, ou réglez le sur quelque chaîne n'ayant pas de sens.

<div class="note">
<h5>SVP, rendez compte des problèmes que vous croisez !</h5>
<p>Si vous croisez un bug, SVP <a href="{{ site.repository }}/issues/new">créez un issue</a> sur GitHub décrivant le problème et tous les contournements que vous avez trouvés avin que nous puissions le documenter ici pour les autres.</p>
</div>
