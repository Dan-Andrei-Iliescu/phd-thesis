# PhD Viva

Damon said to focus on what the importance and impact is.


A Bayesian Approach to dealing with group differences.

The main contribution is that I propose a general model for grouped data and an associated Variational Autoencoder model. I apply it to different real-world problems.

1. Style-content disentanglement.
2. Missing data imputation/controllable generation.
3. Unsupervised domain adaptation.

1. So I started from this problem of Neural Rendering. 
2. I had a questions: How do we combine information from multiple observations?
3. We have the answer: Use Bayesian Updates.
   1. This is the Group-Instance Probabilistc model.
4. However, Bayesian updates are hard to implement. Easier said than done. Here is a paper showing that RNNs are sensitive to the order in which the information is presented.
5. This is what my PhD is about. How to implement Bayesian updates. 
6. I apply it to three problems:
   1. Style-content disentanglement.
   2. Missing Data imputation.
   3. Supervised learning. Regression and classification.
7. What is the future? Why is there a gap between the theoretical model and the practical implementation. Where is the information lost?
   1. One piece of evidence is 

Key terms:
- Group-Instance Model
- CxVAE
- MICVAE
- Group-Instance Predictor


## Questions

1. What opinion will they have of the thesis?
   1. Pietro is an applied person, he cares about applications.
2. What are the weak points?

Setup

## Viva Notes

- Codebase
- Future directions
- Statistical guarantees