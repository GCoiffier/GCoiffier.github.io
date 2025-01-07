+++
title = "1-Lipschitz Neural Distance Fields"
date="2024-06-20"
published_where="Symposium on Geometry Processing 2024"
published_date="24 June 2024"
authors = "Guillaume Coiffier, Louis Béthune"

thumbnail = "/img/1lipSDF/thumbnail.jpeg"
cover = "/img/1lipSDF/cover.jpeg"

abstract = "Neural implicit surfaces are a promising tool for geometry processing that represent a solid object as the zero level set of a neural network. Usually trained to approximate a signed distance function of the considered object, these methods exhibit great visual fidelity and quality near the surface, yet their properties tend to degrade with distance, making geometrical queries hard to perform without the help of complex range analysis techniques. Based on recent advancements in Lipschitz neural networks, we introduce a new method for approximating the signed distance function of a given object. As our neural function is made 1-Lipschitz by construction, it cannot overestimate the distance, which guarantees robustness even far from the surface. Moreover, the 1-Lipschitz constraint allows us to use a different loss function, called the hinge-Kantorovitch-Rubinstein loss, which pushes the gradient as close to unit-norm as possible, thus reducing computation costs in iterative queries. As this loss function only needs a rough estimate of occupancy to be optimized, this means that the true distance function need not to be known. We are therefore able to compute neural implicit representations of even bad quality geometry such as noisy point clouds or triangle soups. We demonstrate that our methods is able to approximate the distance function of any closed or open surfaces or curves in the plane or in space, while still allowing sphere tracing or closest point projections to be performed robustly."

doi = "http://doi.org/10.1111/cgf.15128"
pdf = "/pdf/1lip.pdf"
supplemental = "/pdf/1lip_supplemental.pdf"
code = "https://github.com/GCoiffier/1-Lipschitz-Neural-Distance-Fields"
award = "Best Paper Award"
slides = "/pdf/1lip_slides.pdf"

math=true
toc=true
+++

## Signed Distance Function

This work aims at computing good quality implicit representation of implicit objects. Instead of relying on discrete structures like point clouds, voxel grid or meshes to represent a geometrical object, those representations define surface and curves as the level set (usually the zero level set) of some function. Among the infinity of continuous functions that can implicitly represent a given an object $\Omega \subset \mathbb{R}^n$, the one that best preserves the properties of $\Omega$ far from its zero level set is the _Signed Distance Function_ (SDF) of $\Omega$, which is defined as:

$$ S\_\Omega(x) = \left[\mathbb{1}\_{\mathbb{R}^n \backslash \Omega}(x) - \mathbb{1}\_{\Omega}(x) \right] \min\_{p \in \partial \Omega} ||x - p||$$

where $\partial \Omega$ is the boundary of $\Omega$.

{{< figure src="/img/1lipSDF/implicit_def.jpeg" 
alt="Definition of an implicit surface" 
num="1"
caption="An implicit surface is defined as the level set of some continuous function. Among all possible functions, the signed distance function best preserves geometrical properties far from the surface." 
style="width:600px;" 
>}}

An important property of SDFs is that they satisfy an _Eikonal equation_:

$$\left\\{ \begin{array}{lll} ||\nabla S(x)|| &= 1 \quad &\forall x \in \mathbb{R}^n \\\\ S(x) &= 0 \quad &\forall x \in \partial \Omega \\\\ \nabla S(x) &= n(x) \quad &\forall x \in \partial \Omega \end{array} \right.$$

Having access to the SDF of an object allows for easy geometrical queries and efficient rendering via [ray marching](https://iquilezles.org/articles/raymarchingdf/). For example, the projection onto the surface of $\Omega$ can be defined as:

$$\pi_\Omega(x) = x - S_\Omega(x) \nabla S_\Omega(x).$$

## Neural Distance Fields

The problem with SDFs is that they are difficult to compute. For simple shapes, they may be computed in closed form (see [this webpage](https://iquilezles.org/articles/distfunctions/) by Inigo Quilez that lists many of them), but they quickly become intractable when the objects grows in complexity. This is why there is an ongoing effort to compute good approximations of SDFs. In particular, the recent domain of _neural distance fields_ proposes to use deep learning to solve this problem. The idea here is to define a neural network $f_\theta : \mathbb{R}^n \rightarrow \mathbb{R}$ that will approximate the SDF. However, this approach has two critical limitations:

1) The neural function is usually trained in a regression setting by fitting the correct values on a dataset of points where the true distance function is known. This implies that the input geometry needs to already be known very precisely for such a dataset to be extracted. In other words, one usually need to know the SDF to compute an approximation of the SDF...

2) The final neural network is an approximation of the SDF, which means that it does not exactly satisfy the Eikonal equation. In practice, this means that the norm of its gradient can be a little less or a little more than 1, even with regularization in the loss function:

{{< figure src="/img/1lipSDF/grad.jpeg"
num=2
caption="Plot of a the gradient norm of neural distance fields on a simple 2D dolphin silhouette. While minimizing the eikonal loss stabilizes the gradient norm, only a Lipschitz network guarantees a unit bound." 
style="width:600px;" 
>}}

Why is this second point a problem? If the gradient exceeds unit norm, there is a risk that the function $f_\theta$ overestimates the true distance, which breaks the validity of geometrical queries like projection on the surface (Fig 3. center). If the implicit function always underestimates the distance (Fig 3. right), iterating the projection process will always yield the correct result at the cost of more computation time.

{{< figure src="/img/1lipSDF/queries.jpeg" 
alt="Projection query on an implicit surface"
num=3
caption="Closest point query on an implicit surface. Underestimating the true distance is a necessary condition for the validity of the query." 
style="width:600px;" 
>}}

In summary, it is desirable that the neural function always underestimate the true distance. In mathematical terms, this boils down to requiring $f_\theta$ to be **1-Lipschitz**, that is:

$$|f_\theta(a) - f_\theta(b)| \leqslant ||b-a|| \quad \forall a,b \in \mathbb{R}^n$$


## Our method

Our method aims at building a neural distance field that is garanteed to preserve geometrical properties far from the zero level set. In particular, we use a $1$-Lipschitz neural network so that the Lipschitz constraint will be satisfied _by construction_. On top of this architecture, we minimize a loss that does not need to know the ground truth distance, thus transforming the usual regression problem in a classification problem. Our method is summarized by this diagram:

{{< figure src="/img/1lipSDF/botijo_pipeline.jpeg" 
alt="Overview of our method"  
num=4
caption="Given an input geometry in the form of an oriented point cloud or a triangle soup, we uniformly sample points in a domain containing the desired geometry. Defining negative samples as points of the geometry and positive samples everywhere else yields an unsigned distance field when minimizing the hKR loss. On the other hand, partitioning samples as inside or outside the shape leads to an approximation of the signed distance function of the object."
style="width:100%;" 
>}}


### Step 1: Sampling

Our method takes as input any oriented geometry $\Omega$. This includes point cloud with normals, triangle soups and surface meshes. The first step is to extract a dataset from the input geometry. We define a domain $D \subset \mathbb{R}^n$ as a loose axis-aligned bounding box of $\Omega$ and sample it uniformly.

### Step 2: Separating the interior and the exterior

The second step is to compute labels $y(x) \in \\{-1,1\\}$ for each sampled point $x$. These labels will indicate if the given point is inside or outside of $\Omega$. We propose to use the _Generalized Winding Number_ as proposed by [Baril et al.](https://www.dgp.toronto.edu/projects/fast-winding-numbers/) and implemented in [libigl](https://libigl.github.io/libigl-python-bindings/igl_docs/#fast_winding_number_for_meshes). Intuitively, the winding number $w_\Omega$ of a surface $\partial \Omega$ at point $x$ is the sum of signed solid angles between $x$ and surface patches on $\partial \Omega$. For a closed smooth manifold, the values amounts at how many times the surface "winds around" $x$, yielding an integer value. When computed on imperfect geometries, $w_\Omega$ becomes a continuous function (Fig.5). Through careful thresholding, it is still possible to determine points that are inside or outside the shape with high confidence.

{{< figure src="/img/1lipSDF/gargoyle.jpeg" 
alt="Field of generalized winding number computed on two representations of a gargoyle model. Top row: clean manifold surface mesh. Bottom row: point cloud." 
num=5
caption="The generalized winding number is a robust way of knowing whether a point is inside or outside some geometrical object. For a clean manifold mesh (top row), the GWN takes integer values and classifies the inside from the outside. For imperfect geometries like oriented point clouds (bottom), the GWN is a continuous function that can be thresholded to recover the inside/outside partition." 
style="width:600px;" 
>}}

Alternatively, one can define $y=-1$ for points on the surface of $\Omega$ and $y=1$ everywhere else. In the end, this will result in an unsigned distance field of the boundary. Doing this also extends our method to open surfaces or curves.

### Step 3: Training a 1-Lipschitz network

Once the labels $y$ have been computed, we define some $1$-Lipschitz architecture to approximate the SDF. $1$-Lipschitz neural networks have been extensively studied in theoretical deep learning for their robustness to adversarial attacks and overfitting. Several architectures that are Lipschitz by construction were designed throughout the years. We use the architecture proposed by [Araujo et al.](https://arxiv.org/abs/2303.03169), although any Lipschitz architecture can be used.

On top of the Lipschitz network, we propose to minimize the _hinge-Kantorovitch-Rubinstein_ (hKR) loss. This binary classification loss was first proposed by [Serrurier et al.](https://openaccess.thecvf.com/content/CVPR2021/html/Serrurier_Achieving_Robustness_in_Classification_Using_Optimal_Transport_With_Hinge_Regularization_CVPR_2021_paper.html). For binary labels $y \in \\{-1,1\\}$, hyperparameters $\lambda>0$ and $m>0$ and density function $\rho(x)$ over $D$, the hKR loss is the sum of two terms:

$$\mathcal{L}\_{hKR} = \mathcal{L}\_{KR} + \lambda \mathcal{L}\_{hinge}^m$$

defined as:

$$\mathcal{L}\_{KR}(f\_\theta,y) = \int\_D -yf\_\theta(x) \\, \rho(x) dx$$
$$\mathcal{L}\_{hinge}^m(f\_\theta,y) = \int\_D \max\left(0, m-yf\_\theta(x)\right)\\,\rho(x)dx.$$

We show in the paper that, under mild assumptions on $\rho$, the minimizer of the hKR loss over all possible $1$-Lipschitz functions is the SDF of $\Omega$ up to an error that is bounded by $m$. This means that minimizing the hKR loss will lead to a very good approximation of the SDF.

## Gallery of results

{{< figure src="/img/1lipSDF/gallery.jpeg" 
alt="Various geometrical objects reconstructed from the zero level set of a trained Lipschitz network" 
num=6
caption="Surface extracted from the zero level set of a 1-Lipschitz network trained with our method. Blue surface correspond to signed distance fields while green ones are unsigned." 
style="width:100%;" 
>}}

{{< figure src="/img/1lipSDF/elephant.jpeg" 
num=7
caption="Robust geometrical queries performed on a Lipschitz neural implicit representation of the elephant model." 
style="width:100%;" 
>}}

## Talk video

{{< youtube 3e5lt7UXjeY >}}

## BibTeX
```bibtex
@inproceedings{coiffier20241,
  title={1-Lipschitz Neural Distance Fields},
  author={Coiffier, Guillaume and B{\'e}thune, Louis},
  booktitle={COMPUTER GRAPHICS forum},
  volume={43},
  number={5},
  year={2024}
}
```
