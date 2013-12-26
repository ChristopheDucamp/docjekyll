---
layout: docs
title: Pages GitHub
prev_section: extras
next_section: deployment-methods
permalink: /docs/github-pages/
---

Les [Pages GitHub](http://pages.github.com) sont des pages publiques web pour les utilisateurs, organisations et dépôts, qui sont hébergées gratuitement sur le domaine 
[github.io](http://github.io) de GitHub ou sur un nom de domaine personnalisé de votre choix. 
Les Pages GitHub sont motorisées en coulisses par Jekyll, aussi outre le fait 
de supporter du contenu HTML régulier, c'est aussi un moyen génial d'héberger gratuitement votre site web motorisé-par-Jekyll.

## Déployer Jekyll sur des Pages GitHub

Les Pages GitHub fonctionnent en regardant certaines branches des dépôts sur GitHub.
Il existe deux types basiques disponibles les **pages utilisateur/organisation** et **les pages-projet**.
Le moyen de déployer ces deux types de sites sont presque identiques, hormis quelques détails mineurs.

### Pages Utilisateur et Organisation

Les pages utilisateur et organisation vivent dans un dépôt GitHub dédié 
uniquement pour les fichiers de Pages GitHub. Ce dépôt doit être nommé après le nom du compte. 
Par exemple, [la page utilisateur du dépôt de @mojombo](https://github.com/mojombo/mojombo.github.io) s'appelle `mojombo.github.io`.

Le contenu provenant de la branche `master` de votre dépôt sera utilisé pour construire et publier le site Pages GitHub, aussi assurez-vous que votre site Jekyll soit bien stocké à cet endroit.

<div class="note info">
  <h5>Les noms de domaine personnalisés n'affectent pas les noms des dépôts</h5>
  <p>
    Les Pages GitHub Pages sont initialement configurées pour vivre sous le 
    sous-domaine <code>nomutilisateur.github.io</code>, c'est donc la raison pour laquelle les dépôts doivent être nommés de cette façon <strong>même si un domaine personnalisé est utilisé</strong>.
  </p>
</div>

### Pages Projet 

À la différence des Pages utilisateur et organisation, les Pages Projet sont 
conservées dans le même dépôt pour lesquelles elles sont destinées, si ce n'est que que le contenu du site est stocké dans une branche spécialement nommée `gh-pages`.
Le contenu de cette branche sera restitué en utilisant Jekyll, et l'*output* sera disponible sous un sous-chemin de votre sous-domaine de pages utiliateur, tel que 
`nom-utilisateur.github.io/projet` (à moins qu'un domaine personnalisé ne soit spécifié plus bas).

Le dépôt du projet Jekyll lui-même est un parfait exemple de cette structure de branche —la [branche master]({{ site.repository }}) contient le véritable projet du logiciel, néanmoins le site web Jekyll (celui que vous regardez à cette  heure) est contenu dans la [branche gh-pages]({{ site.repository }}/tree/gh-pages) du même dépôt.

### Structure de l'URL de la Page Projet 

Parfois, il est agréable de prévisualiser votre site avant de pousser votre branche `gh-pages` sur GitHub. Néanmoins, la structure d'URL de type-sous-répertoire que GitHub utilise pour les Pages Projet complique la bonne résolution des URLs. Voici une approche pour utiliser la structure d'URL de Page Projet GitHub (`nomutilisateur.github.io/nom-projet/`) tout en maintenant la capacité de prévisualiser localement votre site Jekyll.

1. Dans `_config.yml`, réglez l'option `baseurl` sur `/nom-projet` -- remarquez le slash en avant et l'**absence** d'un slash à la fin.
2. Au moment de faire référence à des fichiers JS ou CSS, faites comme suit :
   `{% raw %}{{ site.baseurl}}/path/to/css.css{% endraw %}` -- remarquez le slash suivant immédiatement la variable (juste avant "path").
3. Au moment de produire des permaliens ou des liens internes, faites comme suit : 
   `{% raw %}{{ site.baseurl }}{{ post.url }}{% endraw %}` -- notez qu'il n'y a 
   **pas** de slash entre les deux variables.
4. Pour finir, si vous voulez prévisualiser votre site avant de committer/déployer en utilisant `jekyll serve`, assurez-vous de passer une **chaîne vide** vers l'option `--baseurl`, afin de pouvoir tout visualiser normalement sur `localhost:4000` (sans `/nom-projet` au début) : `jekyll serve --baseurl ''`

Ainsi, vous pouvez prévisualiser votre site localement à partir du site racine sur localhost, mais quand GitHub génère vos pages à partir de la branche gh-pages, toutes les URLs commenceront pas `/nom-projet` et se résoudront proprement.

<div class="note">
  <h5>Documentation Pages GitHub, Aide et Support</h5>
  <p>
    Pour plus d'informations sur ce que vous pouvez faire avec les Pages GitHub, tout comme pour les guides de résolution de problèmes, vous devriez jeter un oeil à la <a
    href="https://help.github.com/categories/20/articles">section d'Aide des Pages GitHub</a>. 
    Si tout échoue, contactez le <a href="https://github.com/contact">Support GitHub</a>.
  </p>
</div>
