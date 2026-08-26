# updates — serveur de mise à jour Joomanji

Servi par GitHub Pages à l'adresse **https://magnytu2.github.io/updates/**

## Les huit produits

| produit | fichier xml | où l'installer |
|---|---|---|
| **Corpus** | [`pkg_corpus.xml`](pkg_corpus.xml) | le site public |
| **Astus** | [`pkg_astus.xml`](pkg_astus.xml) | chaque site |
| **Tikus** | [`pkg_tikus.xml`](pkg_tikus.xml) | usage interne, pas à vendre |
| **Iris** | [`plg_system_iris.xml`](plg_system_iris.xml) | chaque site |
| **Oculus** — module d'administration | [`mod_oculus.xml`](mod_oculus.xml) | le site **central** |
| **Oculus** — tâche planifiée | [`plg_task_oculus.xml`](plg_task_oculus.xml) | le site **central** |
| **Oculus** — client ajax | [`plg_ajax_sitemonitor.xml`](plg_ajax_sitemonitor.xml) | chaque site **surveillé** |
| **Corpus — module de démarrage** | [`mod_corpus_start.xml`](mod_corpus_start.xml) | une fois, puis désinstallable |

**Aucun numéro de version ne figure ici, et c'est volontaire.** Une table de
versions recopiée à la main se périme au premier oubli, et annonce alors le
contraire de la vérité — ce document a affiché pendant six jours des numéros
faux de plusieurs dizaines de versions. La version qui fait foi est celle du
fichier xml lui-même : l'ouvrir, la balise `<version>` est en haut.

## Ce que chaque xml doit respecter

L'adresse du fichier doit correspondre **au caractère près** à celle inscrite
sous `<updateservers>` dans le manifeste de l'extension. Une différence, même un
slash final, et Joomla ne cherche jamais de mise à jour — sans message d'erreur.

La somme `<sha256>` doit correspondre au zip pointé par `<downloadurl>`. Elle
change à chaque version : republier un zip sans refaire la somme casse la mise à
jour pour tout le monde.

Le numéro de version ne recule jamais. Joomla compare d'abord la partie
chiffrée et ne regarde le suffixe `-rc` **que si elle est identique** :
`1.0.0-rc2` est inférieur à `1.8.0-rc1`.

## Deux suites de numéros, et c'est voulu

Les **sept produits vendus** suivent `2.0.x-rc2`. Ce point de départ n'est pas
arbitraire : `1.0.0-rc2` aurait été *inférieur* à Astus 1.4.34-rc1 et à Iris
1.8.0-rc1, et ces installations n'auraient plus jamais rien vu.

**`mod_corpus_start` a sa propre suite**, et il y a droit : il a son propre
`element`, Joomla ne le compare à aucun autre produit. Il est resté en `0.x`
tout le temps de sa construction, puis est passé en **`1.0.0-rc2` le 26 août
2026**, quand il a été jugé prêt pour les sous-domaines de démonstration. Il
porte donc le même suffixe `-rc2` que les autres, sans suivre leur `2.0.x`.

Piège de l'ancienne série, à connaître pour relire les vieux paquets :
`version_compare` lit `0.10.2` comme **supérieur** à `0.9.4` — dix est plus
grand que neuf, ce ne sont pas des décimales.

Ce module est **indépendant du paquet `pkg_corpus`** et n'y entrera pas.

## Fichiers hérités

`corpus.xml` désigne l'ancien template Corpus livré seul. Le produit est devenu
un paquet, `pkg_corpus`, ce qui est un identifiant différent pour Joomla. Ce
fichier ne sert plus à rien — **ne pas s'en servir**.

---

*Publication : voir `PUBLIER.md` à la racine de chaque projet, sur le poste de
Cyrille. Rien ne se dépose ici sans être passé par ces contrôles.*
