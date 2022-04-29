# The Concrete Distribution: A Continuous Relaxation of Discrete Random Variables

```
@article{Maddison2017TheCD,
  title={The Concrete Distribution: A Continuous Relaxation of Discrete Random Variables},
  author={Chris J. Maddison and Andriy Mnih and Yee Whye Teh},
  journal={ArXiv},
  year={2017},
  volume={abs/1611.00712}
}
```

The latent variable is a one-hot vector $z \in \{0, 1\}^D$. Consider an unnormalised parametrisation of the distribution of this categorical variable $(\alpha_1, ... \alpha_D)$ where $\alpha_d \in (0, \infty)$.

## Gumbel-max trick
Consider the random variable 

$$Z_k = \left\{ \begin{array}{l} 1, ~ \mathrm{if} ~ k = \argmax_d [\log \alpha_d - \log( - \log U_d)] \\ 0, ~ \mathrm{else} \end{array} \right.$$

where $U_d \sim \mathrm{Uniform}(0, 1)$. This variable has the density:

$$\mathbb{P}(Z_k = 1) = \frac{\alpha_k}{\sum_{d=1}^D \alpha_d}$$

## Concrete random variables
The derivative of the argmax is 0 except at the state change where it is undefined. We want to relax the argmax such that there is a gradient for training $\alpha$. 

The concrete random variable belong to the simplex $∆^{D-1} = \{\mathbf{x} \in [0, 1]^D | \sum_{i=1}^D x_i = 1\}$ whose vertices are discrete random variables. The variable $X_k$ is computed in the following way:

$$X_k = \frac{\mathrm{exp}((\log \alpha_k + G_k)/\lambda)}{\sum_{d=1}^D \mathrm{exp}((\log \alpha_d + G_d)/\lambda)}$$

where $\lambda$ is the softmax temperature and $G_d = - \log(-\log U_d)$ is a Gumbel variable. This variable approaches the Gumbel-max variable as $\lambda$ decreases:

$$\lim_{\lambda \to 0} X = Z$$

The density of the concrete random variable is

$$\mathrm{Pr}_X (x) = (D-1)! ~ \lambda^{D-1} \prod_{k=1}^D \frac{ \alpha_k x_k^{-\lambda-1}}{\sum_{d=1}^D \alpha_d x_d^{-\lambda}}$$

## Which random variable to treat as a stochastic node?

Which variable is the $z$ term on which the KL divergence is computed? If $X$ is that variable, there are problems with log of 0. If $G$ is that variable, the variational bound will be looser. We propose the following variable

$$Y_k = \frac{\log \alpha_k + G_k}{\lambda} - {\mathrm{L\Sigma E}}_{d=1}^D \left( \frac{\log \alpha_d + G_d}{\lambda} \right)$$

The log density of $X$ is

$$\log \mathrm{Pr}_X (x) = \log((D-1)!) + (D-1)\log \lambda + \sum_{d=1}^D [\log \alpha_d - (\lambda + 1) \log x_d] - D ~ \mathrm{L \Sigma E}_{d=1}^D [\log \alpha_d - \lambda x_d]$$

And we use the same density to compute the KL divergence, just replacing $\log x_d$ with $y_d$.