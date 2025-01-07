+++
title = "Mouette: the python library"
thumbnail = "img/mouette.jpeg" #"https://placehold.co/200x200?text=?"
description = "mouette is my python code for handling meshes and implements the geometry processing algorithms I stumbled upon during my research"
tags = ["code"]
date="2023-01-01"
+++


Mouette is my personal  python library for handling point clouds, polylines, surface and volume meshes. It also contains various geometry processing algorithm I encountered in my work, like shortest-paths, old-school parametrization or frame fields.

Mouette (French for seagull) stands for _Maillages, OUtils Et Traitement auTomatique de la géométriE_ (French for "Meshes, Tools and Geometry Processing").

Source code: [https://github.com/GCoiffier/mouette](https://github.com/GCoiffier/mouette)  

## Installation

Using pip: 
```pip install mouette```

## Overview

Mouette allows to easily load data from various file format and access geometrical primitives

#### Import and Export made simple

```python
import mouette as M

mesh = M.mesh.load("path/to/my/mesh/mesh.obj")
print(mesh.vertices[0])
print(mesh.faces[2])
M.mesh.save(mesh,"path/to/export/mesh.obj")
```

#### Define quantities over meshes and work with it

It is possible to define any quantity on mesh elements

```python
my_v_attribute = mesh.vertices.create_attribute("my_attribute", float) # an attribute storing one floating-point number per vertex
my_v_attribute[3] = 4.

my_f_attribute = mesh.faces.create_attribute("my_attribute", 2, int) # an attribute storing two integers per face
m_f_attribute[2] = [1,3]
```

Attributes can store booleans, integers, floating-point numbers, complex numbers and strings, using the provided python types `bool`, `int`, `float`, `complex` and `str`.

#### Call Geometry Processing Algorithms

```python

ff = framefield.SurfaceFrameField(mesh, "vertices", order=4, verbose=True)
ff.run()
ffmesh = ff.export_as_mesh()
M.mesh.save(ffmesh, "framefield.mesh")
```

See other examples in [this folder](https://github.com/GCoiffier/mouette/tree/main/examples)

#### And much more

See full documentation at https://gcoiffier.github.io/mouette/ (still a Work in Progress)


### Run tests

`python -m pytest tests/`
