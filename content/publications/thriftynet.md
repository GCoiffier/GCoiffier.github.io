+++
title = "ThriftyNets: Convolutional Neural Networks With Tiny Parameter Budget"
date="2021-03-30"
published_where="IoT"
published_date="30 March 2021"
authors = "Guillaume Coiffier, Ghouthi Boukli Hacene, Vincent Gripon"

thumbnail = "/img/thriftynet_thumbnail.jpg"
cover = "/img/thriftynet_cover.jpg"

abstract = "Deep Neural Networks are state-of-the-art in a large number of challenges in machine learning. However, to reach the best performance they require a huge pool of parameters. Indeed, typical deep convolutional architectures present an increasing number of feature maps as we go deeper in the network, whereas spatial resolution of inputs is decreased through downsampling operations. This means that most of the parameters lay in the final layers, while a large portion of the computations are performed by a small fraction of the total parameters in the first layers. In an effort to use every parameter of a network at its maximum, we propose a new convolutional neural network architecture, called ThriftyNet. In ThriftyNet, only one convolutional layer is defined and used recursively, leading to a maximal parameter factorization. In complement, normalization, non-linearities, downsamplings and shortcut ensure sufficient expressivity of the model. ThriftyNet achieves competitive performance on a tiny parameters budget, exceeding 91% accuracy on CIFAR-10 with less than 40 k parameters in total, 74.3% on CIFAR-100 with less than 600 k parameters, and 67.1% On ImageNet ILSVRC 2012 with no more than 4.15 M parameters. However, the proposed method typically requires more computations than existing counterparts."

pdf = "https://www.mdpi.com/2624-831X/2/2/12/pdf"
doi = "https://doi.org/10.3390/iot2020012"
code = "https://github.com/GCoiffier/ThriftyNets"
supplemental = ""
+++
