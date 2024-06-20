+++
title = "1-Lipschitz Neural Distance Fields"
date="2024-06-22"
published_where="Symposium on Geometry Processing 2024"
published_date="22 June 2024"
authors = "Guillaume Coiffier, Louis Béthune"

thumbnail = "/img/1lipSDF_thumbnail.jpeg"
cover = "/img/1lipSDF_cover.jpeg"

abstract = "Neural implicit surfaces are a promising tool for geometry processing that represent a solid object as the zero level set of a neural network. Usually trained to approximate a signed distance function of the considered object, these methods exhibit great visual fidelity and quality near the surface, yet their properties tend to degrade with distance, making geometrical queries hard to perform without the help of complex range analysis techniques. Based on recent advancements in Lipschitz neural networks, we introduce a new method for approximating the signed distance function of a given object. As our neural function is made 1-Lipschitz by construction, it cannot overestimate the distance, which guarantees robustness even far from the surface. Moreover, the 1-Lipschitz constraint allows us to use a different loss function, called the hinge-Kantorovitch-Rubinstein loss, which pushes the gradient as close to unit-norm as possible, thus reducing computation costs in iterative queries. As this loss function only needs a rough estimate of occupancy to be optimized, this means that the true distance function need not to be known. We are therefore able to compute neural implicit representations of even bad quality geometry such as noisy point clouds or triangle soups. We demonstrate that our methods is able to approximate the distance function of any closed or open surfaces or curves in the plane or in space, while still allowing sphere tracing or closest point projections to be performed robustly."

doi = ""
pdf = "pdf/1lip.pdf"
supplemental = "pdf/1lip_supplemental.pdf"
code = "https://github.com/GCoiffier/1-Lipschitz-Neural-Distance-Fields"
+++


See [https://lipschitznetworks.net/](https://lipschitznetworks.net/)