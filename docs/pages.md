---
layout: docs
title: Créer des Pages
prev_section: drafts
next_section: variables
permalink: /docs/pages/
---

Outre le fait de pouvoir [écrire des posts](../posts/), une autre chose que vous pouvez vouloir faire avec votre site Jekyll, c'est de créer des pages statiques. En tirant profit de la manière avec laquelle Jekyll copie les fichiers et répertoires, ceci est facile à faire.

## Page d'accueil

Sur presque toute configuration de serveur web que vous croisez, vous cherchez un fichier HTML appelé (par convention) `index.html` dans le répertoire racine du cite et affichez ça comme page d'accueil. À moins que le serveur web que vous utilisiez ne soit configuré par défaut pour chercher un nom de fichier différent, ce fichier s'activera à l'intérieur de la page d'accueil de votre site web généré par Jekyll.

<div class="note">
  <h5>ProTip™ : Utilisez les layouts sur votre page d'accueil</h5>
  <p>
    Tout fichier HTML sur votre site peut utiliser des layouts, même la page d'accueil. Le contenu commun comme les en-têtes et pieds de pages, sont d'excellents candidats pour l'extraction à l'intérieur d'un layout.
  </p>
</div>

## Où vivent les pages additionnelles

L'endroit où vous posez des fichiers HTML pour les pages dépend de la manière dont vous voulez faire fonctionner les pages. Il existe deux moyens principaux pour créer des pages :

- Placez les fichiers nommés HTML pour chaque page dans le répertoire racine de votre site.
- Créez un répertoire dans la racine du site pour chaque page, et placez un fichier index.html dans chaque répertoire de page.

Les deux méthodes fonctionnent bien (et peuvent être utilisés l'une et l'autre), la seule véritable différence étant les URLs résultantes.

### Fichiers HTML nommés

Le moyen le plus simple d'ajouter une page est simplement d'ajouter un fichier HTML dans le répertoire racine avec un nom adapté pour la page que vous voulez créer. Pour un site avec page d'accueil, une page à propos et une page contact, voici à quoi pourraient ressembler le répertoire racine et les URLs associés :

{% highlight bash %}
.
|-- _config.yml
|-- _includes/
|-- _layouts/
|-- _posts/
|-- _site/
|-- about.html    # => http://exemple.com/about.html
|-- index.html    # => http://exemple.com/
└── contact.html  # => http://exemple.com/contact.html
{% endhighlight %}

### Répertoires nommés contenant des fichiers HTML index

Il n'y a rien de faux avec la méthode du dessus, néanmoins certaines personnes préfèrent conserver leurs URLs libres de trucs comme les extensions de noms de fichier. Pour obtenir des URLs propres pour les pages utilisant Jekyll, vous devez simplement créer un répertoire pour chaque page du niveau le plus haut que vous désirez, et puis placer un fichier `index.html` dans chaque répertoire de page. De cette façon, l'URL de la page finit par prendre le nom du dossier, et le serveur web servira le fichier `index.html`. 
Voici un exemple d'une telle structure :

{% highlight bash %}
.
├── _config.yml
├── _includes/
├── _layouts/
├── _posts/
├── _site/
├── about/
|   └── index.html  # => http://exemple.com/about/
├── contact/
|   └── index.html  # => http://exemple.com/contact/
└── index.html      # => http://exemple.com/
{% endhighlight %}

Cette approche peut ne pas correspondre à tous. Mais pour les personnes qui aiment les URLs propres, c'est simple et ça fonctionne. 
La décision finale vous appartient ! 