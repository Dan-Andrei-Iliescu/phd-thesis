# One Datapoint is Not Enough: Disentangling Group-Confounded Data

This is the first time I'm presenting this research, so it will be fun.

GID methods assume for simplicity that the instance encoder is inferred independently for every datapoint. This is appropriate for some datasets where disentanglement is easy

However, we believe this is actually preventing GID from becoming the go-to solution for a wider range of problems that we call group-confounded.

How can we recognise group confounding? $p(v | x, u_1) \neq p(v | x, u_2)$ in the generative model.

We show how changing the relative strength of the group-confounded component in the data affects the performance gap between the conditional and unconditional model.

We generate the score of student $i$ on test $j$:

$$s_{ij} = 2\alpha_i - (\beta_i^2 - 1) \delta_{j} + \epsilon_{ij}$$
- $\alpha_i, \beta_i \sim \mathcal{N} (0, 1)$ - student effect (aptitude)
- $\delta_{j} \sim \mathcal{N} (0, 1)$ - test effect (difficulty)
- $\epsilon_{ij} \sim \mathcal{N} (0, 0.1)$ - variability in the performance

This dataset is obviously group-confounded, since 
$$p(\delta_{j} | s_{ij}, \alpha_i, \beta_i) = \mathcal{N} \left(\frac{s_{ij} - 2\alpha_i}{\beta_i^2 - 1}, 0.1\right)$$

We can also see this in a diagram.

We take the deceptively simple step of conditioning our instance encoder on the previously inferred group variable. We achieve this by concatenating the group code with the input observation.

We think we should be able to achieve better performance on the MDI task if we slightly change the instance encoder. There is a class of problems on which we think GID can achieve much better results. Collaborative filtering is an example of a group confounded task.

A primer on Variational Autoencoders. We train a generative model using a variational latent posterior.

The conditional model is actually the correct factorisation of the generative latent posterior. So we hope that by using the correct factorisation we stand a chance in 

Disentanglement is the goal that a representation network produces separate representations for the factors of variation in the data, such that each representation captures only the variation of its corresponding ground-truth factor. We assume the data has been generated through the interaction of some ground-truth factors. The goal of disentanglement is to represent each factor separately in its own representation.

Group-instance disentanglement is a subclass of this problem where there are 2 ground-truth factors, and the data is grouped according to the values of one of them (so you get groups where that factor has the same value). We call that the group factor, and the other the instance factor.

The way this problem is approached in the literature is through variational autoencoders. You define a decoder that implements a generative model that mimics the ground-truth process. Then you train it using amortised variational inference by defining an encoder (which is one network or a bunch of networks).

