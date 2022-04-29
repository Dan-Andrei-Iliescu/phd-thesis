# Matrix Factorization Techniques for Recommender Systems

Estimate score with dot products of latent variables

$$\hat{r}_{ij} = q_i^T p_j$$

Error is 

$$\min_{q, p} \sum_{i, j} ||r_{ij} - q_i^T p_j||^2 + \lambda(||q_i||^2 + ||p_i||^2)$$

Train with SGD or alternating least squares