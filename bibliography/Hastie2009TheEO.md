# The Elements of Statistical Learning

[Book link](Hastie2009TheEO.pdf)

### 7.2 Bias and Variance

We create a random variable $\mathcal{T}$ modelling the realization of the training data. $\hat{f}$ is the r.v. modelling the estimated function mapping $x$ to $y$. $L$ is the loss function, which, in our case, could be the likelihood given the trained model.

We model the prediction error as:

$$\mathbb{E}_{X', Y'} [L(Y', \hat{f} (X')) | \mathcal{T} = (x, y)]$$

which is in our case

$$\mathbb{E}_{X', Y'} [\mathrm{Pr}_\theta (Y' | X') | \mathcal{T} = (x, y)]$$

A related quantity is the expected prediction error:

$$\mathbb{E}_{X', Y', \mathcal{T}} [ - \log \mathrm{Pr}_\theta (Y' | X') | \mathcal{T}]$$

It does not seem possible to estimate conditional error effectively, given only the information in the same training set.

### 7.3 The Bias-Variance Decomposition

Bias is $\mathbb{E}_{\mathcal{T}} [(\hat{f} (x') - f(x'))^2]$, Variance is $\mathbb{E}_{\mathcal{T}} [(\hat{f} (x') - \mathbb{E}_{\mathcal{T}}[\hat{f} (x')])^2]$

In other words 

