# Interview with Apple Music

I'm interviewing with Matt, who could be either the ML engineer or the head of the group, and Antoine, who I don't yet know. It's a 30 minutes interview and they want to know why I like Music Information Retrieval, what research I have done related to recommender systems, MIR or audio processing, and whether this internship would be a good fit for me.

## TODO
- [ ] I have to find a reason to be interested in MIR.
- My main expertise is in Recommender Systems.
  - [x] What part of recommender systems is my focus?
    - collaborative filtering.
  - [x] What are the challenges in Recommender Systems?
    - sparsity of the ratings matrix, how to embed item information, how to generalize the trained model to new items and users, expressivity of the decoder.
  - [x] What are the current approaches?
    - neighbourhood models, matrix factorization (singular value decomposition), item embeddings, graph convolutional neural networks
  - [x] What have I contributed?
    - fast inference of representations, nonlinear decoder, can generalize to novel items and users, another way of applying the VAE, measure of uncertainty through translation.
    - connected this to domain adaptation and missing value imputation in multilevel models
    - under review at ICML 2022.
  - [x] What would I like to work on in the future?
    - embedding item information in the item representation 
- [ ] How does sequence disentanglement fit into this?
  - Future work on embedding item information in the item representation

Also, what do I want to ask them?
- What venues do you publish in? Are you interested in pure machine learning?
- What are the current research projects?
- What are you excited about?

## Recommender Systems

Ridge regression is regression + a squared loss on the weights: $\hat{\theta} = (\mathbf{X}^T \mathbf{X} + \alpha \mathbf{I})^{-1} \mathbf{X}^T \mathbf{y}$

[Collaborative filtering for recommender systems](https://api.semanticscholar.org/CorpusID:10537313) introduce the matrix factorization framework (singular value decomposition) for collaborative filtering and the Alternating Least-Squares Loss. The loss is:

$$\min_{x,y} \sum_{u, i} (r_{ui} - \mathbf{x}_u^T \mathbf{y}_i) + \lambda (||\mathbf{x}||^2 + ||\mathbf{y}||^2)$$

If we fix either x or y, then it becomes a least squares problem which can be solved analytically. It can also be solved using gradient descent.

Other methods are nearest neighbour. Rating is taken as a weighted average of neighbouring items for that user.

[Factorization Meets Item Embeddings](https://api.semanticscholar.org/CorpusID:1196797) regularizes the training of the item embeddings using item co-occurence similar to word2vec.

[VAEs for CF](https://api.semanticscholar.org/CorpusID:3361310) use a Variational Autoencoder to model the multinomial distribution over items of each user.

[Graph Convolutional Networks](https://api.semanticscholar.org/CorpusID:36809545) use a GCN encoder to produce the embeddings and then a bilinear decoder to recover the ratings.

## MIR
[Downbeat Tracking](https://api.semanticscholar.org/CorpusID:231802311) Kernel is the dot product between scaling coefficients and a learned filter. Disentangling timbral pattern and tempo. Scaling tensor is a spars cube musical time x listening time x scale.

[Factorized Hierarchical VAE](https://api.semanticscholar.org/CorpusID:39395448),  [Disentangled Sequential Autoencoders](https://api.semanticscholar.org/CorpusID:48353305) can separate between local effects (utterances) and global invariants (voice). It can translate between a male voice and a female voice.