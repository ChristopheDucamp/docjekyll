---
layout: docs
title: Guide de démarrage rapide
prev_section: home
next_section: installation
permalink: /docs/quickstart/
---

Impatient ?  Voici comment construire et faire tourner un site Jekyll tous-terrains et *passe-partout*.

{% highlight bash %}
~ $ gem install jekyll
~ $ jekyll new monblog
~ $ cd monblog
~/monblog $ jekyll serve
# => naviguez maintenant vers http://localhost:4000
{% endhighlight %}

Ceci n'est rien néanmoins. La véritable magie opère quand vous commencez à créer des posts de blog, à utiliser le front-matter pour contrôler les gabarits et layouts, et en tirant partie de toutes les merveilleuses options de configuration offertes par Jekyll.

<div class="note info">
  <h5>Redcarpet est le moteur Markdown par défaut pour les nouveaux sites</h5>
  <p>Dans Jekyll 1.1, nous avons basculé le moteur markdown par défaut vers Redcarpet pour les sites générés avec <code>jekyll new</code></p>
</div>

Si vous rencontrez des problèmes, assurez-vous d'avoir tous les [pré-requis 
installés][Installation].

[Installation]: /docs/installation/
