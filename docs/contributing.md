---
layout: docs
title: Contribuer
prev_section: upgrading
next_section: history
permalink: /docs/contributing/
---

Vous avez une idée géniale à jeter dans Jekyll ? Super ! Gardez en tête ce qui suit : 

* Si vous créez une petite réparation ou un patch pour une fonctionnalité existante, un simple test fera simplement l'affaire. SVP, confinez-vous à la suite actuelle de test et utilisez [Shoulda](http://github.com/thoughtbot/shoulda/tree/master) et [RR](http://github.com/btakita/rr/tree/master).
* Si c'est une toute nouvelle fonctionnalité, assurez-vous de créer une nouvelle fonctionnalité [Cucumber](https://github.com/cucumber/cucumber/) et refaites les étapes si nécessaire. Fournissez aussi un peu de documentation dans votre `site` forké, ce sera apprécié. Une fois fusionnée, elle sera tranférée sur le `site` principal, jekyllrb.com.
* Si votre contribution change quelque comportement de Jekyll, assurez-vous de mettre à jour la documentation. Elle vit dans `site/docs`. S'il manque de l'information dans les docs, sentez-vous libre d'en ajouter. Les documentations géniales font les grands projets ! 
* SVP, suivez le [Guide de Style GitHub Ruby](https://github.com/styleguide/ruby) quand vous modifiez le code Ruby.
* SVP, faites de votre mieux pour proposer de **petites pull requests**. Plus la modification proposée est facile à réviser, plus elle a de chance d'être fusionnée.
* Au moment de proposer une pull request, faites SVP un usage judicieux du contenu de la pull request. Une description des changements qui ont été produits, les motivations derrière les modifications et [toutes les tâches achevées ou laissées pour achèvement](http://git.io/gfm-tasks) accéléreront le temps de révision.

<div class="note warning">
  <h5>Les contributions sans tests ne seront pas acceptées</h5>
  <p>
    Si vous créez une petite réparation ou un patch pour une fonctionnalité existante, un petit test simple suffira.
  </p>
</div>

Dépendances Test
---------------------------

Pour faire tourner la suite test et construire la gem, vous devrez installer les dépendances de Jekyll. Jekyll utilise Bundler, faites donc un lancement rapide de la commande `bundle` et tout sera réglé !

{% highlight bash %}
$ bundle
{% endhighlight %}

Avant de démarrer, faites tourner les tests et assurez-vous qu'ils passent (pour confirmer que votre environnement est configuré proprement) :

{% highlight bash %}
$ bundle exec rake test
$ bundle exec rake features
{% endhighlight %}

Workflow
-----------

Voici le moyen le plus direct pour que votre travail soit fusionné dans le projet : 

* Forkez le projet.
* Clonez votre fork localement :

{% highlight bash %}
git clone git://github.com/<nomutilisateur>/jekyll.git
{% endhighlight %}

* Créez une branche thématique qui contient votre modification : 

{% highlight bash %}
git checkout -b ma_fonctionnalite_geniale
{% endhighlight %}


* Hackez, ajoutez les tests. Pas nécessairement dans cet ordre.
* Assurez-vous que tout passe encore en faisant tourner `rake`.
* Si nécessaire, rebasez vos commits à l'intérieur de pièces logiques, sans erreurs.
* Poussez la branche sur le serveur : 

{% highlight bash %}
git push origin ma_fonctionnalite_geniale
{% endhighlight %}

* Créez une demande de pull sur mojombo/jekyll:master et décrivez ce que fait votre modification et pourquoi vous pensez qu'elle devrait être fusionnée.

Mise à Jour de la Documentation
-------------------------------

Nous voulons que la documentation Jekyll soit la meilleure qui soit. Nous avons open-sourcé nos docs et nous souhaitons la bienvenue à toutes les demandes de pull si vous trouvez qu'il existe des manquements.

Vous pouvez trouver la documentation de jekyllrb.com dans le répertoire du 
[site]({{ site.repository }}/tree/master/site) du repo de Jekyll sur GitHub.com.

Toutes les demandes de pull sur la documentation devraient être dirigées sur `master`.  Les requêtes pull dirigées sur une autre branche ne seront pas acceptées.

Le [wiki Jekyll]({{ site.repository }}/wiki) sur GitHub peut être librement mis à jour sans pull request car tous les utilisateurs de GitHub y ont accès.

Pigé !
-----

* Si vous voulez secouer la version gem, placez-la svp dans un commit séparé. De cette façon, les mainteneurs peuvent contrôler quand la gem est mise à jour.
* Essayez de maintenir votre(s) patch(es) basés à partir du dernier commit sur mojombo/jekyll. Plus il sera facile d'exécuter votre travail, moins il y aura de travail pour les mainteneurs, ce qui est toujours une bonne chose.
* SVP, ne taguez pas votre problématique GitHub avec \[fix\], \[feature\], etc. Les mainteneurs lisent activement les problèmes et l'étiquetteront une fois qu'ils l'auront étudiée.

<div class="note">
  <h5>Faites-nous savoir ce qui pourrait être amélioré !</h5>
  <p>
    Utiliser et hacker Jekyll devrait rester amusant, simple et facile. Si pour quelque raison que ce soit, vous trouvez que c'est pénible, <a
    href="{{ site.repository }}/issues/new">créez SVP un "issue"</a> décrivant votre expérience afin que nous puissions l'améliorer.
  </p>
</div>