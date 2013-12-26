---
layout: news_item
title: 'Sortie Jekyll 1.3.0'
date: 2013-11-04 21:46:02 -0600
author: mattr-
version: 1.3.0
categories: [release]
---

Cela fait environ six semaines depuis la v1.2.0 et l'équipe Jekyll 
est heureuse d'annoncer l'arrivée de la v1.3.0. C'est une realease **géante** pleine d'un tas
de toutes sortes de nouvelles fonctionnalités, réparations de bugs, et autres choses que vous 
allez sûrement adorer.

Voici quelques trucs que nous pensons que vous voudrez découvrir dans cette release : 

* Vous pouvez ajouter des [données arbitraires][] au site en ajoutant des fichiers 
  YAML sous un répertoire du site `_data`. Ceci vous permettra d'éviter la répétition 
  dans vos gabarits et de paramétrer les options spécifiques au site sans modifier 
  `_config.yml`.

* Vous pouvez maintenant lancer `jekyll serve --detach` pour initialiser un serveur 
  WEBrick en tâche de fond. **Note:** vous devrez lancer `kill [server_pid]` pour fermer 
  le serveur. Une fois lancé, vous receverez une id de processus que vous pourrez utiliser 
  au lieu de `[server_pid]`

* Vous pouvez maintenant **désactiver les extraits-automatiquement-générés** si vous réglez 
  `excerpt_separator` sur `""`.

* Si vous migrez des pages et posts, vous pouvez maintenant vérifier les **conflits d'URL** en faisant tourner `jekyll doctor`.

* Si vous êtes un fan de la fonctionnalité drafts, vous serez heureux d'apprendre que nous avons ajouté 
  `-D`, une version raccourci de `--drafts`.

* Les permaliens avec des caractères spéciaux devraient maintenant pouvoir être générés sans erreurs.

* Expose la version en cours de Jekyll sous la variable Liquid `jekyll.version`.

Pour une liste complète, visitez notre [change log](/docs/history/)!

[données arbitraires]: /docs/datafiles/
