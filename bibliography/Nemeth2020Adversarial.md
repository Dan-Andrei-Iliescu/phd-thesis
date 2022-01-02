# Adversarial Disentanglement with Grouped Observations
**Link:** https://api.semanticscholar.org/CorpusID:210472540
**Autor:** Jozsef Nemeth
**Subiect:** [[group_instance_disentanglement]]

## Recapitulation of [[bouchacourt_2018]]
- Dataset of grouped observations $\textbf{x}^n = \{x_1^n, ..., x_{K_n}^n\}$ for $n = 1:N$ and $K_n = |\textbf{x}^n|$
	- $x_i^n \in \mathbb{R}^d$ is the $i$-th member of the $n$-th group
- Each group has a content, each instance has a style
- Evidence Lower Bound for a **group** is $$\text{log} ~ p(\textbf{x}) \geq \text{E}_{q(c,\textbf{s}|\textbf{x})} \sum_{i=1}^K \text{log} ~ p(x_i|c, s_i) - \sum_{i=1}^K \text{KL} [q(s_i|x_i) || p(s_i)] - \text{KL} [q(c|\textbf{x}) || p(c)]$$
	- This is the same as my model, right? **No, because their style variable is not sampled conditionally based on the content encoding**
- The problem is content accumulation. They define $$q(c|\textbf{x}) = \frac{1}{Z} \prod_{i=1}^K q(c|x_i)$$
- Apparently, [[hosoya_2019]] has another method for accumulating which is simpler but less correct

## Adversarial disentanglement 
- The accumulation of content information discourages the content variable from learning style information. There is, however, no such barrier for the individual syle variables from learning content information. [[hosoya_2019]] addresses this by limiting the number of dimensions in the style code. Adversarial disentanglement is for minimizing content information in the style code.
	- Experimental results show that larger groups result in better disentanglement. But for smaller groups, the content variable is almost completely ignored.
	- They also show that stronger regularization on the style variable does help disentanglement but at the cost of the overall model performance.
- The content information in $s_i$ can be measured as the mutual information between it and the other observations in the group $I(q(s_i) || q(\textbf{x}_{-i}))$. This should be minimized.
	- They express the mutual information between data samples and style representations as 
    $$I(x;s) = \text{KL} [r(x,s) || \overline{r}(x,s)] = \mathbb{E}_{r(x,s)} ~ \text{log} \frac{r(x,s)}{\overline{r}(x,s)}$$ 
    where $r(x,s) = r(s|x)r(x)$ and $\overline{r}(x,s) = r(x)r(s)$. In other words, $r$ is the joint distribution of a data observation and the style variable conditioned on every other data observation from the group. We define 
    $$r(s|x_i^n) = \frac{1}{K_n - 1} \sum_{j=1,j \neq i}^{K_n} q(s|x_j^n)$$ 
    Also, it is proven that $r(x) = q(x) = p_D(x)$
	> This distribution actually means sampling the style code from any of the other observations in the group, **but not on all the other observations in the group**. What is the difference between these two?
	- This mutual information term can be estimated with a parametric neura estimator [[belghazi_2018]] because it is possible to generate samples from both $r(x,s), \overline{r}(x,s)$.
		- To sample $r(x,s)$ choose a group $\textbf{x}^n$ then choose two observations at random $x_i^n, x_j^n$. Pick $x := x_i^n$ and $s \sim q(s_j^n|x_j^n)$.
		- To sample $\overline{r}(x,s)$ choose two groups $\textbf{x}^m, \textbf{x}^n$. Choose a random observation from each group $x_i^m, x_j^n$. Pick $x := x_i^m$ and $s \sim q(s_j^n|x_j^n)$.
	- Basically the discriminator is learning to tell apart pairs of `(obs, inst_var)` from the same group or from different groups, and the encoder has to make them indistinguishable (basically make the instance variables independent of the grouping). **This is fine, the only problem is that the group cannot be ascertained from individual observations.**
- They approximate the mutual information using desity-ratio training [[belghazi_2018]] [[nguyen_2010]]. The discriminator $T$ is trained to **maximize** 
$$\mathbb{E}_{r(x,s)} [T(x,s)] - \text{log} ~ \mathbb{E}_{\overline{r}(x,s)} [e^{T(x,s)}]$$ 
  - Notice that for the second term the log is in front of the expectation. This means we have to first sample a bunch of $(x,s)$ pairs and then compute the loss.

## Evaluation
- They used 3 datasets: MNIST, Chairs and VGGFace2. They split each dataset into 3 groups: one for training the VAE, one for training the classifier, and the third for testing.
- For quantitative evaluation, they train an SVM classifier on the content and style embeddings to see how well they predict the ground-truth attributes
- For qualitative evaluation they perform translation (switching latents)
- They compare with ML-VAE [[bouchacourt_2018]] and [[jaiswal_2018]]