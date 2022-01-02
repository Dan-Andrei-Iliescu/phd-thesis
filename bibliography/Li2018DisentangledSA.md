# Disentangled Sequential Autoencoder

[Semantic Scholar](https://api.semanticscholar.org/CorpusID:48353305)

They define a generative model of sequential data $[x_i]_{i=1}^n$ as 
$$p(x_{1:k}| f, z_{1:k}) = p(x_{1:k}| f, z_{1:k-1}) ~ p(x_k | f, z_{1:k})$$

They mention there are two possible approximate latent posteriors (given the data). They also mention this method stems from [Jordan, 1999](https://api.semanticscholar.org/CorpusID:2073260)
1. A factorized posterior
2. A full posterior