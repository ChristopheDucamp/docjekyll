---
layout: docs
title: Usage Basique
prev_section: installation
next_section: structure
permalink: /docs/usage/
---

Le gem Jekyll produit un exécutable `jekyll` disponible pour vous dans votre fenêtre de Terminal. Vous pouvez utiliser ces commandes de différentes manières :

{% highlight bash %}
$ jekyll build
# => Le répertoire en cours sera généré à l'intérieur de ./_site

$ jekyll build --destination <destination>
# => Le répertoire en cours sera généré à l'intérieur de <destination>

$ jekyll build --source <source> --destination <destination>
# => Le répertoire <source> sera généré à l'intérieur de <destination>

$ jekyll build --watch
# => Le répertoire en cours sera généré à l'intérieur de ./_site,
#    regardé pour des modifications et regénéré automatiquement.
{% endhighlight %}

Jekyll vient aussi avec un serveur intégré de développement qui vous permettra de prévisualiser à quoi ressemblera le site généré localement dans votre navigateur.

{% highlight bash %}
$ jekyll serve
# => Un serveur de développement fonctionnera sur http://localhost:4000/

$ jekyll serve --detach
# => Même chose que `jekyll serve` mais détachera à partir du terminal en cours.
#    Si vous n'avez pas besoin de killer le serveur, vous pouvez lancer `kill -9 1234` où "1234" est le PID.
#    Si vous ne savez pas trouver le PID, alors faites, `ps aux | grep jekyll` et killez l'instance. [En savoir plus](http://unixhelp.ed.ac.uk/shell/jobz5.html).

$ jekyll serve --watch
# => Même chose que `jekyll serve`, mais cherche les modifications et régénère automatiquement.
{% endhighlight %}

Ce ne sont que quelques-unes des [options de configuration](../configuration/) disponibles.
Beaucoup d'options de configuration peuvent être spécifiées soit comme des flags sur la ligne de commande, ou alternativement (et plus communément) elles peuvent être spécifiées dans un fichier `_config.yml` placé à la racine du répertoire source. Jekyll utilisera automatiquement les options à partir de ce fichier quand il tourne. Par exemple, si vous placez les lignes suivantes dans votre fichier `_config.yml` :

{% highlight yaml %}
source:      _source
destination: _deploy
{% endhighlight %}

Alors les deux commandes qui suivent seront équivalentes : 

{% highlight bash %}
$ jekyll build
$ jekyll build --source _source --destination _deploy
{% endhighlight %}

Pour en savoir plus sur les options possibles de configuration, voir la page 
[configuration](../configuration/).
