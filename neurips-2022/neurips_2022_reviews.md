# Reviews of Group Disentanglement Under Conditional Shift

## Official Review of Paper10236 by Reviewer Hjig

### Summary:
This paper aims at learning separate representations for within- and across- group varitions for a collection of data points. This paper mostly focuses on one case study, the fair comparison between students who attend different schools. Prior works tend to learn separately the school factor and the individual factors. But this paper claims the sampling of individual factors should also depend on the school factor. So the sampling process of this paper first draws the school sample and then sample the instance according to both the input and the school sample for posterior. The resulting model outperforms other baselines in reconstruction error, translation error and mutual information gap.

### Strengths And Weaknesses:
#### Pros:

1. The general idea is succinct to follow and the method is described in a succinct way. The school student performance experiment is also impactful generally.
2. The related works are clearly stated. This paper draws the connections with the prior disentangled sequential VAE where the static (group) and dynamic (individual) factors are to be disentangled [1, 2] and the group/individual disentanglments [3]. This paper did good in connecting with related work, but could further compare the details, as well as the similarities and differences, to better shape the context.

### Cons:

1. The notations are often confusing. If you want to use both $n$ and $K_n$ in the subscripts, you could add a comma to make it more clear. Also, if you want to simplify some notations like in Eq. (2), pls first give the full formula and then specify which subcripts you will omit.
   
<mark>Write full notation!</mark>

2. While I understand the motivations behind CxVAE, some formulations are a bit confusing. For instance, the paper aims at disentangling the group factor and instance factors, and conditioning the instance factor on the group factor. However, an extreme case is that $u_n$ contains most of the information of $v_{n,k}$ and $x_{n,k}$ acts as a look-up key. In this case, $u_n$ and $v_{n,k}$ are completely entangled. Prior works enforce the disentanglement by extracting group factor $u_n$ and instance factor $v_{n,k}$ separately and reconstruct $x_{n,k}$ with both $u_n$ and $v_{n,k}$. In CxVAE, I don't see explicit formuation to encourage the disentanglement. 

<mark>Why does inferring the instance variable conditional on the group variable encourage disentanglement? It's paradoxical.</mark>

3. This wouldn't be reflected in MIG. More precisely, let's say $u$ contains all the information of $v,b,c$ and $v$ has nothing to do with $b,c$. The MIG is still very high, but $u$ and $v$ are entangled. Performance-wise, it is ok. But if your goal is disentanglement, this argument is a bit self-contradictory. If you want to model the dependency between $v_{n,k}$ and $u_n$ while minimize the overlapped information, you could regularize the mutual information between them.

<mark>Why can the group variable not contain the instance information? Why is the information gap a convincing metric?</mark>

4. The pure scores are still less convincing since its dimensionality is low. And students performance should not only be evaluated by scores, let alone the dataset is synthetic. I would be better if you can use some existing datasets like dSprites for your validation and demonstrate the capability.

<mark>Use existing datasets for evaluation, like dSprites.</mark>

5. In Figure 3 and 4, you can compare with more methods like beta-VAE, beta-TCVAE, etc. The paper would become more convincing if you include some other real-world experiments as well.
   
[1] Han, J., Min, M.R., Han, L., Li, L.E. and Zhang, X., 2020, September. Disentangled Recurrent Wasserstein Autoencoder. In International Conference on Learning Representations.

[2] Bai, J., Wang, W. and Gomes, C.P., 2021. Contrastively disentangled sequential variational autoencoder. Advances in Neural Information Processing Systems, 34, pp.10105-10118.

[3] Mathieu, E., Rainforth, T., Siddharth, N. and Teh, Y.W., 2019, May. Disentangling disentanglement in variational autoencoders. In International Conference on Machine Learning (pp. 4402-4412). PMLR.

<mark>Check this paper.</mark>

### Questions:
1. When the sampling of $v_{n,k}$ depends on $u_n$, I think it already means they are entangled?
2. Could you add back the subscript $n$ for clarifications?
3. Could you show more disentanglement metrics? especially the ones to measure the within and across group factors?
4. Have you considered to encode the conditional shift into the instance variation $v_{n,k}$?

### Limitations:
I believe the school performance experiment is a simplified toy example, under the synthetic formulation of Eq. 8-12. More experiments on the mainstream datasets like the ones you listed Shapes3D, dSprites, Cars3D, MPI3D would make your work more persuasive.
Notations could be made more clearly and the superscripts, subscripts should be more consistent.

- Ethics Flag: No
- Soundness: 3 good
- Presentation: 3 good
- Contribution: 2 fair
- Rating: 3: Reject: For instance, a paper with technical flaws, weak evaluation, inadequate reproducibility and incompletely addressed ethical considerations.
- Confidence: 3: You are fairly confident in your assessment. It is possible that you did not understand some parts of the submission or that you are unfamiliar with some pieces of related work. Math/other details were not carefully checked.
- Code Of Conduct: Yes

## Official Review of Paper10236 by Reviewer q1Q4 

### Summary:
The authors proposed a variational inference methods for group-disentangled representation learning. For this purpose, this paper mainly focuses on a case study on the problem of fair comparisons between students who attend different schools. The main difference from prior work such as GVAE and ML-VAE is that, their proposed method assume conditional dependency between group-level variables and instance-level variables in the inference model, while GVAE or ML-VAE assume independence between them.

### Strengths And Weaknesses:
Strengths:

In general I think it is interesting to study the disentangled representation learning in hierarchical models, because there are many use cases there the generative models have this group structure. Also, this paper is pretty clear about most of the points and I can easily understand the details of the propose methods.

Weaknesses:

- While they provide detailed analysis in one case study, I would expect that they evaluate their propose inference method in more complicated data modalities such as image datasets that were used in prior work. To make an apple-to-apple comparison, I wonder how it performs against the baselines in the same experiments from prior work.

<mark>To make and apples-to-apples comparison, test on image datasets like previous works.</mark>

- I don't fully understand why adding the dependency between group-level variables and instance-level variables can help to better disentangle the latent representations. Prior work such as GVAE or ML-VAE tried to achieve disentanglement by enforcing independence between group-level and instance-level variables. With the conditional dependency that is proposed in this paper, these variables by construction should be correlated, thus be entangled with each other. Then how can you justify that the inference method will necessarily result in disentangled representations?

<mark>How can conditioning the instance variable on the group variable result in disentangled representations?</mark>

- The authors need to discussion more recent related work. For example, [1, 2] also learn group-level representations with the same type of generative models. So I would expect the authors can include these papers in their discussion and talk about how their work differ from each of these.

[1] Abid, Abubakar, and James Zou. "Contrastive variational autoencoder enhances salient features." arXiv preprint arXiv:1902.04601 (2019).

[2] Severson, Kristen A., Soumya Ghosh, and Kenney Ng. "Unsupervised learning with contrastive latent variable models." Proceedings of the AAAI Conference on Artificial Intelligence. Vol. 33. No. 01. 2019.

<mark>Check these papers.</mark>

- Questions: Please see my questions in the previous section.
- Limitations: The authors have discussed the limitations of their work. To my best knowledge, there is no obvious negative societal impact of their work.
- Ethics Flag: No
- Soundness: 2 fair
- Presentation: 3 good
- Contribution: 2 fair
- Rating: 4: Borderline reject: Technically solid paper where reasons to reject, e.g., limited evaluation, outweigh reasons to accept, e.g., good evaluation. Please use sparingly.
- Confidence: 4: You are confident in your assessment, but not absolutely certain. It is unlikely, but not impossible, that you did not understand some parts of the submission or that you are unfamiliar with some pieces of related work.
- Code Of Conduct: Yes

## Official Review of Paper10236 by Reviewer vryR

### Summary:
In this paper, the authors aim to address the problem of group disentanglement. Considering a special case of fair comparisons between students who attend different schools, the existing methods fail to learn the disentangled representation, so the authors address this limitation by conditioning the instance encoder 13 of the GVAE on the group representation. The authors evaluate the performance of the proposed method in the simulated dataset of test scores.

### Strengths And Weaknesses:
There are some concerns as follows:

The authors claim that the proposed method is based on the conditional shift. According to [1][2], the latent variables are the cause of x, which is different from the causal graph shown in Figure 1.

<mark>The reviewer is confusing the inference model with the generative model.</mark>

The contribution of this paper is limited. It seems that the author just straightforwardly combines the causal graph with the variational encoder. 

The authors do not provide the identification theory for the proposed method like [3].

<mark>In what cases can the causal model be uniquely identified?</mark>

The proposed method is a general method, but the authors only evaluate it on the simulated dataset. Why do the authors evaluate it on the other datasets or other downstream tasks like domain adaptation or domain generalization?



It is suggested that the authors should provide more implementation detail of the proposed method.

<mark>Provide more implementation details.</mark>

[1] Domain Adaptation under Target and Conditional Shift 

[2] Domain Adaptation with Conditional Transferable Components

[3] Self-Supervised Learning with Data Augmentations Provably Isolates Content from Style

<mark>This paper presents an identification theory that I should use.</mark>

### Questions:
Please refer ''Strengths And Weaknesses''

### Limitations:
Please refer ''Strengths And Weaknesses''

- Ethics Flag: No
- Soundness: 2 fair
- Presentation: 2 fair
- Contribution: 2 fair
- Rating: 3: Reject: For instance, a paper with technical flaws, weak evaluation, inadequate reproducibility and incompletely addressed ethical considerations.
- Confidence: 5: You are absolutely certain about your assessment. You are very familiar with the related work and checked the math/other details carefully.
- Code Of Conduct: Yes

## Official Review of Paper10236 by Reviewer N45Q

### Summary:
The paper is well-written, the problem is well-justified and the method isn't unnecessarily complicated and the performance looks very good. However, they have focused on one special dataset, and a more rigorous experiment section is needed.

### Strengths And Weaknesses:
The paper is well-written, the problem is well-justified and the method isn't unnecessarily complicated and the performance is very good.

### Questions:
no questions

### Limitations:
As mentioned in the conclusion section their method is evaluated against only one synthetic dataset. I am not an expert in this field but I think this is the biggest limitation of their work.

- Ethics Flag: No
- Soundness: 3 good
- Presentation: 4 excellent
- Contribution: 3 good
- Rating: 4: Borderline reject: Technically solid paper where reasons to reject, e.g., limited evaluation, outweigh reasons to accept, e.g., good evaluation. Please use sparingly.
- Confidence: 2: You are willing to defend your assessment, but it is quite likely that you did not understand the central parts of the submission or that you are unfamiliar with some pieces of related work. Math/other details were not carefully checked.
- Code Of Conduct: Yes