+++
title = "Visualizing Frame Fields"
description = "A demo of the frame fields algorithms implemented in mouette using Polyscope"
thumbnail = "img/FF_polyscope/cad.jpeg"
tags = ["code"]
date="2024-06-12"
math=true
toc=true
+++

This project is a small demo of some of the frame field algorithms that I implemented over time. The code is available [on github]() if you want to try it out.

## What is frame field ?


## Applications of frame fields

More recently, frame fields have been developed in the context of quad-remeshing. The idea is that they "abstract away" the combinatorics of a quadmesh and define the flow lines of the future edges. Also, their singularities correspond to the irregular vertices in the quadmesh (more on that later).

## Computing a smooth frame field

$$\min \sum_{a \sim b} w_{ab} ||v_b - \exp(\imath r_{ab})\\, v_a ||^2 \quad \quad (1)$$
subject to constraints that $v$ should be fixed on the boundary and one of its branch should be tangent. Here, $w_{ab}>0$ are weight terms and $r_{ab} \in (-\pi ; \pi)$ is the angle of the parallel transport between $a$ and $b$. Applying this correction is essential to take the natural curvature of the surface into account.

## Singularities of a frame field

## The demo

The demo displays the algorithms we implemented in [mouette]().

The demo uses the [Polyscope]() library to display results from 

{{< figure src="/img/FF_polyscope/bunny.jpeg" 
alt="" 
caption="Stanford bunny"
style="width:80%;" 
>}}


{{< figure src="/img/FF_polyscope/cad.jpeg" 
alt="" 
caption="CAD model"
style="width:80%;" 
>}}

## See also

- Survey
- Directional Library