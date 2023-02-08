# ICLR 2023 Reviews

## Reviewer sLYB

### Summary Of The Paper:

The paper proposes a context aware variational auto encoder which modified the structure of previous C-VAE. The evaluation is on synthetic data only.

### Strength:

- the work touches a fundamental problem.

### Weakness:

- Only synthetic experiments are conducted.
- The VAE only tested with MLP.
- The data generated is in low dimensional and not very persuasive.

### Clarity, Quality, Novelty And Reproducibility:

- The paper is clear, but lacking of intuition. For example, why we need to add $u_n$ into distribution for $Q$? Any intuition for doing that?
- What is the proof detail for eqn 8-10? Some equation is wield. Eqn 3-4 are also the same equation.
- It is unclear how to implement the proposed ELBO loss in real world? Which reparameter trick are you using?
- Why the method was only tested in synthetic data? How about high dimensional real world images? For example, the GVAE tested in image data. It is conventional to show in some real world high dimensional data.

### Summary Of The Review:

I think the paper is lacking of intuition and details at this stage. In addition, the experiment is insufficient (only synthetic data used).

Correctness: 2: Several of the paper’s claims are incorrect or not well-supported.
Technical Novelty And Significance: 3: The contributions are significant and somewhat new. Aspects of the contributions exist in prior work.
Empirical Novelty And Significance: 2: The contributions are only marginally significant or novel.
Flag For Ethics Review: NO.
Recommendation: 5: marginally below the acceptance threshold
Confidence: 2: You are willing to defend your assessment, but it is quite likely that you did not understand the central parts of the submission or that you are unfamiliar with some pieces of related work. Math/other details were not carefully checked.

## Reviewer G1Wn

### Summary Of The Paper:

The paper makes a simple modification to the parameterized posterior distribution to allow for learning group-representations and the within-group instance representation when they are dependent conditional on the observed features: condition the instance representations on both the features and the group representation. As the paper puts it, this can handle conditional shift where changing the group changes the instance representation for the same features.

### Strengths:

- Simple modification to the posterior affords good advantanges.- - Promising performance on synthetic data.

### Weaknesses:

My main concern with the paper is acknowledged by the authors but nonetheless remains important: "The main limitation of our work is that we perform evaluation on a synthetic dataset of student scores rather than real data."

I do not think such an evaluation can be avoided. Reconstruction error is the one metric that I can trust and that to me only sounds like a part of the story in the paper. Translation additionally seems to be important but I do not see it evaluated on real data.

Important questions include:

- What is the point out the translation metric if it cannot be evaluated on real data? The authors say "Our model preserves the relative positions of the scores" in figure 2. It this something we desire naturally or something that comes out of an assumption?

- How can we guarantee relative positions of the features when translating without restrictions on q?

- What the desiderata for disentanglement here without stating the method? How should one evaluate them?
- The definition of conditional shift seems to say "changing the group changes the instance representation for the same features.". This is a natural consequence of conditioning on the collider as in figure 1 first figure (assuming a causal graph). Why call it conditional shift when it's a consequence of the assumed data generating process?

### Clarity, Quality, Novelty And Reproducibility:

The paper is written well. The idea is simple and exists in prior work, but the novelty seems to be in using the group-representation-conditioning to better learn instance representations.

### Summary Of The Review:

The paper is written well, but it remains to be seen whether the proposed method is useful for any real datasets.

Correctness: 2: Several of the paper’s claims are incorrect or not well-supported.
Technical Novelty And Significance: 3: The contributions are significant and somewhat new. Aspects of the contributions exist in prior work.
Empirical Novelty And Significance: 3: The contributions are significant and somewhat new. Aspects of the contributions exist in prior work.
Flag For Ethics Review: NO.
Recommendation: 3: reject, not good enough
Confidence: 3: You are fairly confident in your assessment. It is possible that you did not understand some parts of the submission or that you are unfamiliar with some pieces of related work. Math/other details were not carefully checked.

## Reviewer iRs6

### Summary Of The Paper:

The paper tackles the problem of group disentanglement in presence of conditional shift. This work proposes a new group disentanglement method called the Context-Aware Variational Autoencoder. Experiments on toy datasets show that the proposed method can significantly improve over existing methods.

### Strengths

Paper tackles an important and relevant problem

### Weaknesses

- Results are present only on the toy dataset in the paper. This is the biggest weakness of the paper. Moreover, since the data-generating process is also proposed in the paper, it is unclear if the dataset is specially designed that can show the failure modes of other methods and if those failure modes are present in other real-world datasets.
- Since all the experiments are on toy datasets, the claims made in the abstract and introduction are overstated. For example, "Our model has the novel ability to disentangle ambiguous observations". There is no concrete evidence in the paper when this will hold and how general of a statement this is?
- Tackling the problem of conditional shift is very general and ill-posed. It is unclear from the writing how the paper deals with inherent underspecification.
- Method description in Section 4 is a bit skim. Equations 8-10 appear to be a bit out of the place and it is unclear how the text above these equations follows.
- Only the toy dataset is considered in the paper. Any description evaluation criterion is missing. It is hard to understand the tasks considered in Figures 3 and 4.
- Reproducibility statement is not present and No code is provided as well. Authors can use the 9th page in the main paper and additional appendices to provide those details.

### Clarity and Writing issues

- Overall the writing in the introduction is not easy to follow. There is no clear flow between problems tackled in the paper, issues with the existing works, and contributions of the paper.
- The writing in contribution bullets is a bit hard to follow. The first bullet " We approach the task of learning fair representations of students from different schools/socio-economic backgrounds." appears to be a bit disconnected from the previous sentence.
    "conditional shift directly causes our model’s improvement in performance over existing methods", is a bit misleading. This statement can not be true in general without the additional assumptions on what is not shifting. Moreover, the sentence structure is also unnecessarily complex.

### Reproducibility concern

- Code or detailed experiment setting is not provided in the paper.
- Moreover, no hyperparameter details are shared

### Summary Of The Review:

Overall, the writing of the paper is very unclear and the proposed method is only evaluated on toy datasets. It is also unclear how the inherent underspecification of conditional shift is handled in the paper.

Correctness: 2: Several of the paper’s claims are incorrect or not well-supported.
Technical Novelty And Significance: 2: The contributions are only marginally significant or novel.
Empirical Novelty And Significance: 2: The contributions are only marginally significant or novel.
Flag For Ethics Review: NO.
Details Of Ethics Concerns: Not applicable
Recommendation: 3: reject, not good enough
Confidence: 4: You are confident in your assessment, but not absolutely certain. It is unlikely, but not impossible, that you did not understand some parts of the submission or that you are unfamiliar with some pieces of related work.

## Reviewer KtA6

### Summary Of The Paper:

This paper proposed a novel group entanglement method under the concern of conditional shift in dataset. In the paper, the author argues that under the conditional shift, the group representation and instance representation cannot be inferred independently since the instance distribution is confounded by the group identity. The proposal is to control the group variable while learning the individual representation. This paper claims to be the first in unsupervised group disentanglement to condition on group variables while learning the individual variables.

### Strength

The major strength of this paper can be summarized in the following aspects:

- This paper correctly points out the weakness of existing methods in group disentanglement when the conditional shift exists. The idea that the group variables are confounders when inferring the individual variables is important to know.
- Learning disentangled representation to handle the conditional shift is relatively new since as the paper stated, most methods focus on learning invariant representation under the shift.
- The synthesis examples are easy to follow and it demonstrates the impact of conditional shift over existing group entanglement methods

### Weakness

The major weakness of this paper can be summarized in the following aspects:

- The idea of conditioning/controlling on group variables when inferring the individual variables is not novel. It follows naturally by the definition of conditional shift, i.e. the group conditional distribution of instances are different. As the paper points that it is widely used in semi-supervised learning. The innovation point is its use in unsupervised learning and generative models. However, it is not sufficient to meet the bar for ICLR.
- One of main concerns for the conditioning method is when it deals with high dimensional problems. In high dimensional space, conditioning would restrict the set of samples that are available to the model in each group. Note that this method essentially learns a set of group specific models. In high dimensional setting, the generative model needs a lot more samples generated before a robust inference result is obtained. This is partially why the conditional independence assumption was used, since it would save a lot of time in data generation.
- That being said, the experiments are too simple. It is a low dimensional example, while the high dimensional data set such as image dataset are mentioned but not tried. It is important to demonstrate the strength and weakness of this method in high dimensional setting, esp the time for inference and the robustness of the inference.
- No code provided. Although this is not hard to implement, it is better to have some code to prove the reproducibility.

### Clarity, Quality, Novelty And Reproducibility:

The paper is well written with clear demonstration of the problem and solution. The work is partially original but there are many existing models using the similar ideas. The code is not available thus cannot demonstrate its reproducibility.

### Summary Of The Review:

In sum, this paper provides an interesting perspective on the group entanglement under conditional shift. The solution is intuitive and easy to follow. However, the idea is not very novel since it has been explored in many tasks before. It also fails to demonstrate its strength and weakness under more realistic and high dimensional dataset.

Correctness: 4: All of the claims and statements are well-supported and correct.
Technical Novelty And Significance: 2: The contributions are only marginally significant or novel.
Empirical Novelty And Significance: 2: The contributions are only marginally significant or novel.
Flag For Ethics Review: NO.
Recommendation: 3: reject, not good enough
Confidence: 5: You are absolutely certain about your assessment. You are very familiar with the related work and checked the math/other details carefully.


## Rebuttal

We thank the reviewers for their careful reading of the paper and for their insightful and constructive comments. We agree with the majority of their comments and we recognise the need for substantially updating this paper.

In our updated paper, we focused on fixing the main limitation identified by the reviewers: the lack evaluation on high-dimensional datasets. To address this, we tested our model on the 3DIdent ( https://arxiv.org/abs/2102.08850 ) dataset, a popular dataset for evaluating disentanglement that also exhibits conditional shift. We observe our model producing a significant improvement in disentanglement over prior work. The new results can be seen in Section 6.

We also agree with the many useful secondary comments that we did not manage to address in time for the rebuttal deadline. Those will be our main focus for the next version of the paper:

- The need for more intuitive explanation of why conditioning on the group variable is necessary.
- Adding a code repository to the supplementary material that would allow readers to reproduce the experiments.
- A discussion of the assumptions of conditional shift and a formalisation of the space of problems we are considering.

In the new version of the paper, we also make a few small corrections pointed out by the reviewers.

- Added optimiser hyperparameters in the "Model Setup" section.
- Used a single number to label multi-line equations.
