# Variational Autoencoder with Arbitrary Conditioning

[Semantic Scholar](https://api.semanticscholar.org/CorpusID:67855732)

**TL;DR They propose a modification of the variational autoencoder which allows for conditioning on an arbitrary subset of the input space in a one-shot fashion.**

- Learn all conditional distributions of the form $p(x_U | x_{D \backslash U})$ where $D$ is the total number of features and $U$ are the missing features.
- They apply their method to two real use-cases, feature imputation and image inpainting.

## Related Work

The [Universal Marginalizer](https://api.semanticscholar.org/CorpusID:30363134) trains a single neural network to approximate the marginal distribution of any subset of features given any other subset of features.

## Problem Statement

The goal is to build a model of the conditional distribution $p_D (x_b | x_{1-b}, b)$, where $b \in \{0, 1\}^D$ and $x_b$ is the subset of features from $x$ indicated by $b$. They use a distribution $p_\theta$ to approximate this. *However, because the true distribution is intractable, the parametric distribution has to prioritize certain $b$s over others.*
 
> This observation is very interesting, because the implemented distribution cannot match the true one, we need to prioritize certain samples over others.


