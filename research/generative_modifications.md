# Sequential Generative Modifications

- Diffusion models learn the inverse of a corruption process.
- Start from a set of given images, then learn which modifications preserve the image manifold.
  - The modifications depend on what the starting image is.
  - This is like turning an isotropic Gaussian into a multivariate Gaussian.
    - Find the function describing the covariance matrix.
- Like a random walk through the image manifold.
