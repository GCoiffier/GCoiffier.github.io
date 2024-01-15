+++
title = "PhD Thesis: Global Parametrization Algorithms for Quadmeshing"
date="2023-12-06"
thumbnail = "/img/phd_thumbnail.jpg"
cover = "/img/phd_cover.jpg"

published_where = "Université de Lorraine"
published_date="6 December 2023"

pdf = "https://hal.univ-lorraine.fr/tel-04346473v1"
+++

This work was supervised by [Dmitry Sokolov](https://members.loria.fr/DSokolov/) and [Etienne Corman](https://members.loria.fr/ECorman/).

The defense occurred on December 6th 2023 at the Université de Lorraine.

### Jury

- [Xavier Goaoc](https://members.loria.fr/Xavier.Goaoc/), Université de Lorraine [President]
- [Mirela Ben-Chen](https://cris.technion.ac.il/en/persons/mirela-ben-chen), Technion Israel Institute of Technology [Reviewer]
- [Marco Tarini](https://tarini.di.unimi.it/), University of Milan [Reviewer]
- [Bruno Lévy](https://brunolevy.github.io/), Inria, Centre de l'Université de Lorraine
- [Pooran Memari](http://www.lix.polytechnique.fr/~memari/), CNRS, Ecole Polytechnique
- [Mélina Skouras](https://imagine.inrialpes.fr/people/mskouras/index.htm), Inria, Centre de l'Université de Grenoble
- [Etienne Corman](https://members.loria.fr/ECorman/), CNRS, LORIA [Advisor]
- [Dmitry Sokolov](https://members.loria.fr/DSokolov/), Université de Lorraine [Advisor]

### Abstract
Quadrangular meshes are a central data structure in the domain of geometry processing, with applications ranging from computer graphics to numerical simulation. A promising approach for automatic generation of high quality quadmeshes relies on the observation that they consist in a deformation of the regular grid almost everywhere, except at a few singular vertices. Thanks to the computation of a parametrization, that is to say a flat representation, of the surface to be meshed, it is then possible to overlay a grid to be lifted back as a quad mesh. For quads to be extracted from this surface parametrization, it has to be seamless, that is to say satisfy a set of alignment constraints on its boundary and its cuts. This needs a quantization as integer values of some of its degrees of freedom. These constraints are usually enforced progressively in a well-studied pipeline of operations, consisting in the computation of a smooth frame field, defining the future singular vertices of the mesh, an integration phase from which a rotationally seamless parametrization is recovered, and a quantization step to determine the translational degrees of freedom.