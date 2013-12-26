---
layout: docs
title: Bonus
prev_section: plugins
next_section: github-pages
permalink: /docs/extras/
---

Il existe un certain nombre de fonctionnalités bonus (optionnelles) supportées par Jekyll que vous pourriez avoir envie d'installer, selon votre plan d'utilisation de Jekyll.

## Support LaTeX

Maruku vient avec un support optionnel de LaTeX vers un rendu PNG via blahtex
(Version 0.6) qui doit être dans votre `$PATH` aux côtés de `dvips`. Si vous avez 
besoin de Maruku pour ne pas supposer un endroit fixé pour `dvips`, regardez le 
[fork Maruku de Remi](http://github.com/remi/maruku).

## RDiscount

Si vous préférez utiliser [RDiscount](http://github.com/rtomayko/rdiscount) au lieu de [Maruku](http://github.com/bhollis/maruku) pour Markdown, assurez-vous de l'installer :

{% highlight bash %}
$ [sudo] gem install rdiscount
{% endhighlight %}

Puis allez dans votre fichier `_config.yml` et spécifiez RDiscount comme moteur Markdown afin que Jekyll tourne avec cette option.

{% highlight yaml %}
# In _config.yml
markdown: rdiscount
{% endhighlight %}

## Kramdown

Vous pouvez aussi utiliser [Kramdown](http://kramdown.rubyforge.org/) au lieu de Maruku
pour Markdown. Assurez-vous que Kramdown soit installé :

{% highlight bash %}
$ [sudo] gem install kramdown
{% endhighlight %}

Ensuite vous pouvez spécifier Kramdown comme moteur Markdown dans `_config.yml`.

{% highlight yaml %}
# Dans _config.yml
markdown: kramdown
{% endhighlight %}

Kramdown a différentes options pour personnaliser l'output HTML. La page 
[Configuration](/docs/configuration/) liste les options par défaut utilisées par 
Jekyll. Une liste complète des options est aussi disponible sur le [site web Kramdown](http://kramdown.rubyforge.org/options.html).
