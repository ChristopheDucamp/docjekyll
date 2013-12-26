---
layout: news_item
title: 'Jekyll 1.4.2 Released'
date: 2013-12-16 19:48:13 -0500
author: parkr
version: 1.4.2
categories: [release]
---

Cette release réparer [une régression][] où les blocs de code fenced de Maruku ont été désactivés, 
au lieu de la valeur précédente par défaut sur on. 
Nous avons ajouté une nouvelle configuration par défaut 
à notre clé de config `maruku` : `fenced_code_blocks` et l'avons 
réglé par défaut sur `true`.

Si vous ne souhaitez pas utiliser les blocs de code fenced  de Maruku, 
vous pouvez désactiver cette option dans votre fichier de configuration du site.


[une régression]: https://github.com/jekyll/jekyll/pull/1830
