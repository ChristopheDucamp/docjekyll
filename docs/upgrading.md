---
layout: docs
title: Mettre à jour
prev_section: resources
next_section: contributing
permalink: /docs/upgrading/
---

Mise à jour à partir d'une version plus ancienne de Jekyll ? Quelques trucs ont changé dans la version 1.0 que vous pourriez vouloir connaître.

Avant de plonger, allez récupérer la dernière version de Jekyll :

{% highlight bash %}
$ gem update jekyll
{% endhighlight %}

<div class="note feature">
  <h5 markdown="1">Plongeon</h5>
  <p markdown="1">Vous voulez consruire et faire tourner rapidement un nouveau site Jekyll ? Faites tourner simplement <code>jekyll new NOMDUSITE</code> pour créer un nouveau répertoire avec les fondations de site Jekyll.</p>
</div>

### La Commande Jekyll

Pour plus de clarté, Jekyll accepte désormais les commandes `build` et `serve`. Alors qu'avant vous pouviez uniquement tourner la commande `jekyll` pour générer un site et lancer `jekyll --server` pour le voir localement, utilisez désormais les sous-commandes `jekyll build` et `jekyll serve` pour faire la même chose. Et si vous voulez que Jekyll reconstruise automatiquement à chaque fois le site lorsqu'un fichier est modifié, ajoutez simplement à la fin de la commande le flag `--watch`.

<div class="note info">
  <h5>Regarder et Servir</h5>
  <p markdown="1">Avec les nouvelles sous-commandes, la façon dont les sites sont prévisualisés change un peu. Au lieu de spécifier `server: true` dans le fichier de configuration du site, utilisez `jekyll serve`. La même chose s'applique pour `watch: true`. Au lieu de cela, utilisez le flag `&#45;&#45;watch` avec soit `jekyll serve` ou `jekyll build`.</p>
</div>

### Permaliens Absolus

Dans Jekyll v1.0, nous avons introduit les permaliens absolus pour les pages dans les sous-répetoires. Jusqu'à la v2.0, c'était en **opt-in**. À partir de la v2.0, néanmoins, les permaliens absolus deviendront **opt-out**, c'est à dire que Jekyll utilisera par défaut des permaliens absolus au lieu de permaliens relatifs.

* Pour utiliser des permaliens absolus, allez dans votre fichier de configuration et réglez `relative_permalinks: false`.
* Pour continuer à utiliser des permaliens relatifs, réglez dans votre fichier de configuration `relative_permalinks: true`.

<div class="note warning" id="absolute-permalinks-warning">
  <h5 markdown="1">Les permaliens absolus seront activés par défaut dans la v2.0</h5>
  <p markdown="1">
    À partir de la Jekyll v2.0, `relative_permalinks` sera réglé par défaut sur `false`, ce qui veut dire que toutes les pages seront construites en utilisant le comportement de permalien absolu. La bascule existera encore jusqu'à la v2.0.
  </p>
</div>

### Posts Draft

Jekyll vous permet désormais d'écrire des posts brouillons, et vous permet de les prévisualiser avant publication. Pour commencer un draft, créez simplement un répertoire appelé `_drafts` dans le répertoire source de votre site (par ex. à côté de `_posts`), et ajoutez-lui un nouveau fichier markdown. Pour prévisualiser votre nouveau post, lancez  simplement la commande `jekyll serve` avec le flag `--drafts`.

<div class="note info">
  <h5 markdown="1">Les drafts n'ont pas de dates</h5>
  <p markdown="1">
    À la différences des posts, les drafts n'ont pas de date, parce qu'ils n'ont pas encore été publiés. Plutôt que de nommer votre draft comme quelque chose de type `2013-07-01-mon-post-brouillon.md`, nommez simplement le fichier que vous aimeriez poster ici comme quelque chose du type `mon-post-brouillon.md`.</p>
</div>

### Personnaliser le Fichier Config

Plutôt que de passer les flags individuels via la ligne de commande, vous pouvez maintenant passer un fichier personnalisé de config Jekyll complet. Ceci aide à faire la distinction entre les environnements, ou vous permet d'écraser les valeurs par défaut spécifiées-par-l'utilisateur. Ajoutez simplement le flag `--config` à la commande `jekyll`, suivi du chemin vers un ou plus fichiers de configuration (délimités par des virgules, pas des espaces).

#### Résultat, les flags de ligne de commande suivants sont désormais dépréciés : 

* `--no-server`
* `--no-auto`
* `--auto` (maintenant `--watch`)
* `--server`
* `--url=`
* `--maruku`, `--rdiscount`, et `--redcarpet`
* `--pygments`
* `--permalink=`
* `--paginate`

<div class="note info">
  <h5>Le flag config spécifie explicitement votre (vos) fichier(s) de config.</h5>
  <p markdown="1">Si vous utilisez le flag `&#45;&#45;config`, Jekyll ignorera votre fichier 
    `&#95;config.yml`. Vous voulez fusionner une configuration personnalisée avec la configuration normale ? Aucun problème. Jekyll acceptera plus d'un fichier personnalisé de config via la ligne de commande. Les fichiers de config sont en cascade de droite à gauche, comme si je fais tourner 
    `jekyll serve &#45;&#45;config &#95;config.yml,&#95;config-dev.yml`,
    les valeurs dans les fichiers config sur la droite (`&#95;config-dev.yml`) écrasent celles sur la gauche  (`&#95;config.yml`) quand les deux contiennent la même clé.</p>
</div>

### Nouvelles Options du Fichier Config

Jekyll 1.0 a introduit de novuelles options du fichier config. Avant de mettre à jour, vous devriez vérifier si celles-ci sont présentes dans votre fichier de config pre-1.0, et si oui, vous assurer de les utiliser proprement :

* `excerpt_separator`
* `host`
* `include`
* `keep_files`
* `layouts`
* `show_drafts`
* `timezone`
* `url`

### Baseurl

Souvent, vous voudrez avoir la capacité de faire tourner un site Jekyll à plusieurs endroits, comme une prévisualisation locale avant de pousser vers les Pages GitHub. Jekyll 1.0 facilite ça avec le nouveau flag `--baseurl`. Pour tirer partie de cette fonctionnalité, ajoutez d'abord la `baseurl` de production à votre fichier du site `_config.yml`. Puis, sur tout le site, préfixez simplement les URLs relatives avec `{% raw %}{{ site.baseurl }}{% endraw %}`. Quand vous êtes prêts pour prévisualiser votre site localement, passez le flag `--baseurl` avec votre url de base (probablement `/`) vers `jekyll serve` et Jekyll remplira dedans tout ce que vous avez passé, vous assurant que vos liens fonctionnent comme attendu dans les deux environnements.


<div class="note warning">
  <h5 markdown="1">Toutes les URLs de page et post contiennent des slashes devant</h5>
  <p markdown="1">Si vous utilisez la méthode décrite au-dessus, rappelez-vous que les URLs pour tous les posts et pages commencent par un slash. Par conséquent, en concaténant la baseurl du site et l'url de post/page où `site.baseurl = /` et `post.url = /2013/06/05/mon-post-fun/` provoquera deux slashes en avant, ce qui brisera les liens. Il est donc suggéré que préfixer avec `site.baseurl` ne soit uniquement utilisé quand la `baseurl` est quelque chose d'autre que la valeur par défaut `/`.</p>
</div>
