---
layout: docs
title: Installation
prev_section: quickstart
next_section: usage
permalink: /docs/installation/
---

Installer Jekyll et le faire tourner ne devrait vous prendre que quelques minutes. 
Si ça devient vraiment douloureux, [poussez une nouvelle problématique]({{ site.repository }}/issues/new) (ou proposez une *pull request*) décrivant le problème que vous avez rencontré et comment nous pourrions faciliter le processus.

### Pré-requis

Installer Jekyll est facile et immédiat, mais voici quelques exigences que vous devrez vous assurer d'avoir dans votre système avant de démarrer.

- [Ruby](http://www.ruby-lang.org/fr/downloads/)
- [RubyGems](http://rubygems.org/pages/download)
- Linux, Unix, ou Mac OS X

<div class="note info">
  <h5>Faire tourner Jekyll sur Windows</h5>
  <p>
    Il est possible de faire 
    <a href="http://www.madhur.co.in/blog/2011/09/01/runningjekyllwindows.html">
    tourner Jekyll sur Windows</a>, mais la documentation officielle ne couvre pas 
    le support d'installation sur les plates-formes Windows.
  </p>
</div>

## Installer avec RubyGems

Le meilleur moyen d'installer Jekyll se fait via 
[RubyGems](http://docs.rubygems.org/read/chapter/3). Dans le terminal, lancez simplement la commande suivante pour installer Jekyll : 

{% highlight bash %}
$ gem install jekyll
{% endhighlight %}

Toutes les dépendances gem de Jekyll sont automatiquement installées par la commande au-dessus, vous n'avez donc pas à vous en inquiéter. Si vous rencontrez des problèmes dans l'installation de Jekyll, regardez la page [problèmes](../troubleshooting/) ou [rapportez le problème]({{ site.repository }}/issues/new) de manière à ce que la communauté Jekyll puisse améliorer l'expérience pour tous.

<div class="note info">
  <h5>Installer les Outils de Ligne de Commande Xcode</h5>
  <p>
    Si vous rencontrez des problèmes à installer des dépendances de Jekyll utilisant des extensions natives et Mac OS X, vous devrez installer Xcode et les Outils de Ligne de Commande associés. Téléchargez à l'intérieur de 
    <code>Preferences &#8594; Téléchargements &#8594; Components</code>.
  </p>
</div>

## Bonus Optionnels

Il existe un certain nombre de fonctionnalités supplémentaires (optionnelles) supportées par Jekyll que vous pourriez vouloir installer selon votre intention d'utilisation de Jekyll. Ces bonus incluent le support de LaTex, et l'usage de moteurs alternatifs de restitution du contenu. 
Regardez la [page extras](../extras/) pour plus d'information.

<div class="note">
  <h5>ProTip™ : Autoriser la Coloration Syntaxique</h5>
  <p>
    Si vous êtes le type de personne qui utilise Jekyll, alors il y a des chances que vous vouliez autoriser la coloration syntaxique en utilisant Pygments. Vous devriez vraiment 
    <a href="../templates/#code_snippet_highlighting">regarder comment faire</a> avant d'aller plus loin.
  </p>
</div>

Maintenant que tout est installé, allons faire fonctionner tout ça ! 
