+++
title = "Parametric Surface Fitting on Airborne Lidar Point Clouds for Building Reconstruction"
date="2021-11-01"

published_where="Computer-Aided Design"
published_date="01 November 2021"
authors = "Guillaume Coiffier, Justine Basselin, Nicolas Ray, Dmitry Sokolov"

thumbnail = "/img/roofit_thumbnail.jpg"
cover = "/img/roofit_cover.jpg"

abstract = " Surface reconstruction is an essential step in most processing pipelines involving point clouds. By constructing a surfacic or volumetric model of the cloud, it is possible to infer large-scale semantic and geometric information required for most applications in computer graphics, simulation and virtual reality. Among the different types of point cloud and the variety of possible problems, we are interested in airborne Lidar data and the problem of building reconstruction for urban planning ranging from flood and light exposure simulation to virtual touristic visits. While most existing reconstruction methods are based on characteristic features extraction in point clouds such as planes, ridges, contours and their combination into a more complex model, we instead adopt a template-based approach relying on a library of complex primitives developed in an industrial context. This is formulated as a global fitting problem between a constrained triangulated mesh (our template) and the point cloud. More precisely, we design an energy function that takes into account the distance between both objects while integrating outliers rejection directly in our numerical optimization through the use of an M-estimator. This energy function being smooth everywhere, it can be efficiently minimized by quasi-Newtonian methods like the L-BFGS algorithm. We demonstrate the reliability of our approach on a collection of diverse roof models and several publicly available Lidar datasets, as well as its robustness and limits in function of initialization, point cloud quality and presence of outliers. By only fitting onto relevant points, this method allows a precise fitting as well as a correct outlier segmentation in a unique step, providing a reasonable initialization close to the barycenter of the cloud. "

doi = "https://dx.doi.org/10.1016/j.cad.2021.103090"
pdf = "https://hal.science/hal-03281816"
+++
