---
layout: docs
title: Travailler avec des drafts
prev_section: posts
next_section: pages
permalink: /docs/drafts/
---

Les drafts sont des posts sans date. Ce sont des posts sur lesquels vous travaillez et que vous ne voulez pas publier. Pour faire fonctionner des  drafts, créez un répertoire `_drafts` à la racine de votre site (comme décrit dans la section [structure du site](/docs/structure/)) et créez votre premier draft :

{% highlight text %}
|-- _drafts/
|   |-- un-post-draft.md
{% endhighlight %}

Pour prévisualiser votre site avec des drafts, faites simplement tourner `jekyll serve` ou `jekyll build` avec le switch `--drafts`.  Chacun d'eux de verra assigner la valeur time de la modification du fichier draft pour sa date, et vous verrez donc les drafts actuellement édités comme les posts les plus récents.
