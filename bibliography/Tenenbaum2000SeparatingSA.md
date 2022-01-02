# Separating Style and Content with Bilinear Models

[Semantic Scholar](https://api.semanticscholar.org/CorpusID:9492646)

**Symmetric Model** They model images as bilinear models
$$x_k = \sum_{i=1}^I \sum_{j=1}^J w_{ijk} s_i c_j$$
where $k$ is the index of the pixel (or feature, for non-image data), $I$ is the dimensionality of the style code $s$ and $J$ is the dimensionality of the content code $c$. $w_{ij}$ is a vector called a basis image.

**Asymmetric Model** In order to give the style vector more expressiveness, they make a separate weight matrix for each style
$$x_k = \sum_{i=1}^I \sum_{j=1}^J w^s_{ijk} s_i c_j$$

The error to be minimized is
$$E = \sum_{n=1}^N \mathbb{I} (s_n = \mathbf{s}) ~ \mathbb{I} (c_n = \mathbf{c}) ~ ||\mathbf{x}^{(n)} - \sum_{k}\mathbf{s}^\intercal \mathbf{W}_k \mathbf{c}||^2$$

In the case of the asymmetric model, $w^s_{ijk}, s_i$ are fixed during the training phase.