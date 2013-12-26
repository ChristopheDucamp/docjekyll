---
layout: docs
title: Fichiers Data
prev_section: variables
next_section: migrations
permalink: /docs/datafiles/
---

En plus des [variables intégrées](../variables/) disponibles dans Jekyll, vous pouvez spécifier vos propres data personnalisées pouvant être accédées via le [système de template Liquid](http://wiki.github.com/shopify/liquid/liquid-for-designers).

Jekyll supporte le chargement de data à partir des fichiers [YAML](http://yaml.org/) situés dans le répertoire `_data`.

Cette fonctionnalité puissante vous permet d'éviter la répétition dans vos templates et de régler des options spécifiques au site sans modifier `_config.yml`. 

Les Plugins/thèmes peuvent aussi tirer partie des Fichiers Data pour régler les variables de configuration.

## Le Répertoire Data

Comme expliqué sur la page [sructure des répertoires](../structure/), le répertoire `_data` 
est l'endroit où vous pouvez stocker de la data supplémentaire à utiliser par Jekyll au moment de générer votre site. Ces fichiers doivent être des fichiers YAM (en utilisant soit l'extensions `.yml` ou `.yaml`) et ils seront accessibles via `site.data`.

## Exemple : Liste de membres

Voici un exemple basique d'utilisation des Fichiers Data pour éviter de copier-coller de grands morceaux de code dans vos templates Jekyll : 

Dans `_data/members.yml`:

{% highlight yaml %}
- name: Tom Preston-Werner
  github: mojombo

- name: Parker Moore
  github: parkr

- name: Liu Fengyun
  github: liufengyun
{% endhighlight %}

Cette data peut être accédée via `site.data.members` (remarquez que le nom du fichier détermine le nom de la variable).

Vous pouvez maintenant restituer la liste des membres dans un template :

{% highlight html %}
{% raw %}
<ul>
{% for member in site.data.members %}
  <li>
    <a href="https://github.com/{{ member.github }}">
      {{ member.name }}
    </a>
  </li>
{% endfor %}
</ul>
{% endraw %}
{% endhighlight %}
