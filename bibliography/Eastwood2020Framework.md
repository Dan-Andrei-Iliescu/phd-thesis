# A Framework for the Quantitative Evaluation of Disentangled Representations

[Semantic Scholar](https://api.semanticscholar.org/CorpusID:19571619)

> *A disentangled representation is generally described as one which separates the factors of variation, explicitly representing the important attributes of the data*

The procedure for evaluating disentanglement is to train a regressor $f$ to predict the true underlying factor $z$ given the latent code $c$. Then, quantify the deviation of $f$ on the testing data.

They use regressors which can provide a matrix of relative importances $R$ where $R_{ij}$ shows the importance of latent component $c_i$ for the factor component $z_j$. This allows to explicitly define and quantify the 3 properties of disentanglement: 

1. **Disentanglement.** This is how separated the representations are. The disentanglement score of code variable $c_i$ is $D_i = (1 - H_K (P_i))$ where $H_K (P_i) = - \sum_{k=0}^{K-1} P_{ik} \log_K P_{ik}$ is the entropy and $P_{ij} = R_{ij} / \sum_{k=0}^{K-1} R_{ik}$ is the probability that unit $c_i$ is relevant for $z_j$ (as opposed to the other $x_k$). *If $c_i$ is important for predicting a single generative factor, the score will be 1. If $c_i$ is equally important for predicting all generative factors, the score will be 0.*
   
   In order to account for dead units, they define the relative code variable importance $\rho_i = \sum_{k} R_{ik} / \sum_{j, k} R_{jk}$. Thus, the overall disentanglement score is a weighted average $\sum_{i} \rho_i D_i$.
2. **Completeness.** The degree to which each underlying factor is captured by a single latent variable. $C_k = (1 - H_D (\tilde{P}_{:k}))$  is the completeness score, $H_D (\tilde{P}_{:k}) = - \sum_{d=1}^D \tilde{P}_{dk} \log_D \tilde{P}_{dk}$ is the entropy and $\tilde{P}_{dk} = R_{dk} / \sum_{e=1}^D R_{ek}$ is the probability that factor $z_k$ is predicted by component $c_d$ (as opposed to other components $c_e$).
3. **Informativeness.** How much information the latent code contains about the underlying generative factor. Measured as the sum of errors between the ground-truth factor and the prediction for each component $\sum_k E(f_k (\mathbf{c}), z_k)$.
