+++
title = "Compactly supported detail field for high quality neural implicit surfaces"
date="2026-01-07"
published_where="Symposium on Geometry Processing (Computer Graphics Forum)"
published_date="2026"
authors = "Guillaume Coiffier, Justine Basselin"

thumbnail = "/img/neural_detail_field/thumbnail.jpeg"
cover = "/img/neural_detail_field/cover.jpeg"

abstract = "Neural implicit surfaces are a powerful tool for encoding a surface as the zero level set of a neural function. Trained using gradient-descent based optimizers, these methods however suffer from a low-frequency bias that prevents them to fit fine details of the surface. Solutions to break this bias exist but often damage the regularity of the long range implicit function, making geometrical queries more difficult. In this work, we combine a 1-Lipschitz neural function with a detail field made of compactly supported radial basis functions. While the neural function handles long-range queries with low surface accuracy, the detail field is fitted to perturb the neural function so that its zero level set precisely goes through sampled points of the surface and locally accounts for small-scale details. As it is compactly supported, regions where the 1-Lipschitz property breaks are finely controlled. We therefore achieve the best of both worlds by greatly increasing the representation power of the implicit function near the zero level set while maintaining robustness far from the zero level set. "

# doi = "http://doi.org/10.1111/cgf.15128"
pdf = "/pdf/neural_detail_field.pdf"
supplemental = "/pdf/neural_detail_field_supplemental.pdf"
code = "https://github.com/GCoiffier/neural-sdf-detail-field"
# slides = "/pdf/"

math=false
toc=false
+++