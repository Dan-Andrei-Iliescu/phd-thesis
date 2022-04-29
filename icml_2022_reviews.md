# Reviews of Phase 1 (rejected)

[Learning Invariant Representations](http://proceedings.mlr.press/v97/zhao19a/zhao19a.pdf)

## Meta review

The novelty of the proposed method is limited, as similar modifications of variational autoencoder exist in the literature. A major weakness of this paper is that the experiments were performed only on synthetic data and that there are no results on real-world data. This decision is based primarily on Reviewer #4's opinion and meta-reviewer's reading of the paper. Although reviewer #3 recommended Phase 2 review, for the ICML community, it is critical to demonstrate the performance of the method on real data.

## Reviewer 3

1. **Summarize the contributions made in the paper with your own words** This paper assumes a situation in which each sample belongs to a group and the sample generating process is affected by both group-specific latent variables and instance-level latent variables conditioned on the group. Existing research assumed that instance-level latent variables were independent of the group.
2. **Novelty, relevance, significance** The authors claim that the novelty of this study is the introduction of instance-level latent variables conditioned on the group. Since the proposed structure of the latent variables is fairly simple, it would not surprise me if this has already been proposed, but as far as I know, this is new.
3. **Soundness** The experimental conditions and results are carefully explained. On the other hand, the learning algorithm for the generative model is not well described. Is it possible to maximize the ELBO based on the posterior distribution, in Equation 7? Is this optimization trivial?
4. **Quality of writing/presentation** There is no problem with writing quality.
5. **Literature** There is no problem with literature.
6. **Basis of review (how much of the paper did you read)?** I read the full paper.
7. **Summary** The learning algorithm for the generative model is not well described. Is it possible to maximize the ELBO based on the posterior distribution, in Equation 7? Is the optimization trivial?
10. **[R] Phase 1 recommendation. Should the paper progress to phase 2?** Yes

## Reviewer 4

1. **Summarize the contributions made in the paper with your own words** This paper tackles group disentanglement - learning separate representations for the group and instance attributes. Differently from other works, it attempts to tackle dataset without requiring the covariate shift assumption i.e. p(y|x,d) != p(y|x,d'). It claims (although we do not agree) that it is the first paper to use a conditional encoder for inferring the instance code. It validates the method using a synthetic dataset proposed by the authors.
1. **Novelty, relevance, significance** 
   1. **Novelty:** I do not believe this work is novel. Conditional encoders have been used before e.g. [1, 2]. I believe that this is the main claimed technical contribution. As this claim is unfounded, this paper cannot be said to be novel. Although claiming to be the first to research the covariate shift assumption - this has been extensively researched in the domain adaptation/generalization literature e.g. [3]
   2. **Significance:** This results of this work are not very significant as the paper is only evaluated on a simple synthetic dataset simulated by the authors. It is not clear that the method works - as it was not demonstrated on realistic datasets. If I hard for me to find an aspect of this paper to have significance for the community. In terms of the list of claimed contribution in Sec.1. Claims 1 and 2 are that conditional encoders are beneficial - however we argued this is not new. Claim 3 is that the analysis of the contributions of conditional encoders is helpful. Although this claim is true, I do not believe it is significant given claims 1 and 2.
      1. [1] Kingma et al., Semi-supervised Learning with Deep Generative Models,, NeurIPS'1
      2. [2] Saito et al., COCO-FUNIT Few-Shot Unsupervised Image Translation with a Content Conditioned Style Encoder, ECCV'20
      3. [3] Zhao, Han, et al. "On learning invariant representations for domain adaptation." International Conference on Machine Learning. PMLR, 2019
   3. **Soundness:** Although I believe conditional encoders indeed have the capability to perform the assigned task, the evaluation is not sound. It is. only performed on a synthetic dataset compiled for the purposes of this paper. it should be performed on realistic datasets. Also as mentioned before, this is not a new idea in disentanglement, making the novelty claims unsound.
2. **Quality of writing/presentation** The paper is well written, but does not utilize two extra pages that could have been used for running more experiments or justifying the difference from the previous work that I highlighted..
3. **Literature**
[1] Kingma et al., Semi-supervised Learning with Deep Generative Models,, NeurIPS'14
[2] Saito et al., COCO-FUNIT Few-Shot Unsupervised Image Translation with a Content Conditioned Style Encoder, ECCV'20
[3] Zhao, Han, et al. "On learning invariant representations for domain adaptation." International Conference on Machine Learning. PMLR, 2019
6. **Basis of review (how much of the paper did you read)?** I read the paper carefully and believe I understood it.
7. **Summary** The paper's main premise is that conditional encoders for the representation will deal better with confounding than unconditional encoders. However, group conditional encoders have been used before [1,2] and so the main technical idea here is not novel. Further, the dataset presented here is a synthetic dataset handcrafted by the authors. Although toy dataset are useful for understanding the method in a controlled environment, the evaluation should be performed on more realistic datasets. Furthermore, as the method is similar to [1], it is not clear to me what new idea is being evaluated here. Due to the novely, significance and soundness concerns, I recommend rejection.
10. **[R] Phase 1 recommendation. Should the paper progress to phase 2?** No