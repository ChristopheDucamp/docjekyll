---
layout: news_item
title: "Jekyll 1.0.1 Released"
date: "2013-05-08 23:46:11 +0200"
author: parkr
version: 1.0.1
categories: [release]
---

Chaud dans la lignée de la v1.0, la v1.0.1 est sortie ! Voici less points forts :

* Ajouté un nouveau préfixe de nom de classe `language-` aux blocs de code ([#1037][])
* Message d'erreur Commander maintenant préféré sur l'abandon du process avec des args incorrects ([#1040][])
* Ne pas forcer l'usage de toc_token au moment de générer une generate_toc dans RDiscount ([#1048][])
* RedCarpet respecte l'option de configuration pygments ([#1053][])
* Réparé la construction d'index avec  LSI ([#1045][])
* N'imprime pas l'avertissement de dépréciation quand aucun argument n'est spécifié. ([#1041][])
* Ajouté `</div>` manquante au gabarit du site utilisé par la sous-commande `new`, réparé les typos dans le code ([#1032][])

Voir la page [Historique][] pour plus d'information sur cette version.

{% assign issue_numbers = "1037|1040|1048|1053|1045|1041|1032" | split: "|" %}
{% for issue in issue_numbers %}
[#{{ issue }}]: {{ site.repository }}/issues/{{ issue }}
{% endfor %}

[Historique]: /docs/history/#101__20130508
