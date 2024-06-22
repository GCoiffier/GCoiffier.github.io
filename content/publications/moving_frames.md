+++
title = "The Method of Moving Frames for Surface Parametrization"
date="2023-09-20"
published_where="Transaction on Graphics"
published_date="20 September 2023"
authors = "Guillaume Coiffier, Etienne Corman"

thumbnail = "/img/moving_frames_thumbnail.jpg"
cover = "/img/moving_frames_cover.jpg"

abstract = "This article introduces a new representation of surface global parametrization based on Cartan’s method of moving frames. We show that a system of structure equations, characterizing the local coordinates changes with respect to a local frame system, completely characterizes the set of possible cone parametrizations. The discretization of this system provably provides necessary and sufficient conditions for the existence of a valid mapping. We are able to derive a versatile algorithm for surface parametrization, allowing feature constraints and singularities. As the first structure equation is independent of the global coordinate system, we do not require prior knowledge of cuts or cone positions. So, a single non-linear least-square problem is enough to place quantized cones while minimizing a given distortion energy. We are therefore able to take full advantage of the link between the parametrization geometry and the topology of its cone metric to solve challenging constrained parametrization problems."

doi = "https://doi.org/10.1145/3604282"
pdf = "https://hal.science/hal-03670525"
code = "https://github.com/GCoiffier/moving_frames_parametrization"
supplemental = "https://homepages.loria.fr/ECorman/Papers/cartan_supp.pdf"
+++


## Bibtex

```latex
@article{coiffier2023movingframes,
	author = {Coiffier, Guillaume and Corman, Etienne},
	title = {The Method of Moving Frames for Surface Global Parametrization},
	year = {2023},
	issue_date = {October 2023},
	publisher = {Association for Computing Machinery},
	volume = {42},
	number = {5},
	issn = {0730-0301},
	url = {https://doi.org/10.1145/3604282},
	doi = {10.1145/3604282},
	journal = {ACM Trans. Graph.},
	month = {sep},
	articleno = {166},
	numpages = {18}
}
```
