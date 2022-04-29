# Variational Autoencoders for Collaborative

## Introduction

In recommender systems, we observe how a set of users interact with a set of items. In collaborative filtering, we make predictions solely based on the patterns of interactions between the users and the items, and no the item content itself.

*Although, it would be interesting to condition on the item.*

Latent factor models measuring the cosine similarity between user and item are still state-of-the-art, although they are inherently linear.

- Implicit feedback - play counts
- Explicit feedback - ratings