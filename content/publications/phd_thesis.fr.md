+++
title = "Manuscrit de thèse : Algorithmes de paramétrisation globale pour maillages quadrangulés"
date="2023-12-06"
thumbnail = "/img/phd_thumbnail.jpg"
cover = "/img/phd_cover.jpg"

published_where = "Université de Lorraine"
published_date="6 Décembre 2023"

pdf = "https://hal.univ-lorraine.fr/tel-04346473v1"
+++

Thèse encadrée par [Dmitry Sokolov](https://members.loria.fr/DSokolov/) et [Etienne Corman](https://members.loria.fr/ECorman/).

Soutenue le 6 décembre 2023 à l'Université de Lorraine.

### Jury

- [Xavier Goaoc](https://members.loria.fr/Xavier.Goaoc/), Université de Lorraine [Président]
- [Mirela Ben-Chen](https://cris.technion.ac.il/en/persons/mirela-ben-chen), Technion Institut de Technologie d'Israel [Rapporteur]
- [Marco Tarini](https://tarini.di.unimi.it/), Université de Milan [Rapporteur]
- [Bruno Lévy](https://brunolevy.github.io/), Inria, Centre de l'Université de Lorraine
- [Pooran Memari](http://www.lix.polytechnique.fr/~memari/), CNRS, Ecole Polytechnique
- [Mélina Skouras](https://imagine.inrialpes.fr/people/mskouras/index.htm), Inria, Centre de l'Université de Grenoble
- [Etienne Corman](https://members.loria.fr/ECorman/), CNRS, LORIA [Encadrant]
- [Dmitry Sokolov](https://members.loria.fr/DSokolov/), Université de Lorraine [Encadrant]

### Résumé

Les maillages quadrangulaires (quads) sont une structure de données centrale au domaine du traitement automatique de la géométrie, trouvant des applications en infographie comme en simulation numérique. Une approche prometteuse pour générer automatiquement des maillages quads de grande qualité s'appuie sur le fait qu'ils constituent une déformation de la grille régulière presque partout, excepté en un petit nombre de points singuliers. Grâce au calcul d'une paramétrisation, à savoir une représentation planaire, de la surface à mailler, il est alors possible d'y tracer une grille qui, reprojetée sur la surface, formera le maillage désiré. Pour que des quadrilatères puissent être extraits, cette paramétrisation se doit d'être \"sans couture\", c'est-à-dire de respecter un ensemble de contraintes d'alignement sur son bord et ses découpes. Ces contraintes sont généralement imposées petit à petit dans un pipeline d'opérations désormais bien étudié, consistant en un calcul de champ de repères lisse, définissant les futurs points singuliers du maillage, une phase d'intégration pour obtenir une paramétrisation aux coutures sans rotation, suivie d'une phase de quantification déterminant les degrés de liberté en translation. Cette thèse s'intéresse à l'amélioration des différentes étapes du pipeline de génération de maillages quadrangulaires. En nous appuyant sur des notions de géométrie différentielle, nous proposons des formulations du problème évitant les écueils de l'approche actuelle. Premièrement, nous abandonnons la résolution de problèmes en nombre entier pour certaines étapes (connue pour être difficiles à résoudre) pour la remplacer par la minimisation de fonctions objectif continues (bien que non convexe). Deuxièmement, nous fusionnons certaines étapes du pipeline en une seule optimisation déterminant en un seul coup les degrés de liberté correspondants. Cela permet plus de versatilité et de contrôle utilisateur sur le maillage quad final, et évite les cas d'échecs classiques causés par l'approche gloutonne du pipeline actuel. Ces formulations théoriques du problème de paramétrisation sans couture s'accompagnent d'implémentations pratiques dans lesquelles nous démontrons la viabilité de nos approches sur une grande variété de modèles CAO. Finalement, notre travail est en théorie généralisable au problème plus difficile du maillage hexaédrique, là où les algorithmes de paramétrisation actuels sont soit uniquement valables pour les surfaces, soit échouent à produire des résultats de façon robuste.
