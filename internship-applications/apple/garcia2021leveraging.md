# Leveraging Hierarchical Structures for Few-Shot Musical Instrument Recognition

```
@inproceedings{Garcia2021LeveragingHS,
  title={Leveraging Hierarchical Structures for Few-Shot Musical Instrument Recognition},
  author={Hugo Flores Garcia and Aldo Aguilar and Ethan Manilow and Bryan Pardo},
  booktitle={ISMIR},
  year={2021}
}
```

## Prompt
Firstly, we would like you to conduct a paper review on this paper.
- There is a **word limit of 300 words**.
- This paper was not chosen as an indication of the internship subject, but simply because it is a good representation of current MIR research.
- We expect you to give a report of the **main contribution** of the paper, the **general context** of its discovery and the potential **weak points**, the potential **applications** and **future work** it would allow both in the context of research but also **applied to Apple Music’s context**.

## Abstract
Hierarchical prototype embeddings classify musical instruments better than non-hierarchical methods in a few-shot settings. They propose a method to aggregate prototypes in such a way as to mirror the predefined hierarchy of musical instruments. Their method also makes less severe mistakes.

## Introduction

We want instrument recognition at every instant during the audio recording, therefore this is a subproblem of event labelling.

People with visual impairment have difficulty identifying the instruments of a music passage, because they cannot see the waveform.

Current methods for musical instrument recognition require large datasets for training, which can only be provided for a few number of very common instruments. Even by curating a diverse dataset, we still want the end user to train the model for a new instrument, a la few-shot.

Organizing musical instruments hierarchically has precedent in human cultures.
This could help the recognition of rare instruments by associating them with more common instruments from the same category.

They propose a hierarchical extension to prototypical networks in order to reflect this hierarchy.

## Related Work

The identity of this paper is that it does few-shot sound event detection using a hierarchical structure.

There is work on implementing hierarchical structures in deep learning. There is work on hierarchical audio classification, but it doesn't work in few-shot cases.There is work on few-shot sound event detection, but non


## Background
### Few shot learning
Assume a dataset split into $|K|$ classes of $|S_k|$ examples each. The task is to classify $M$ unseen samples into one of the classes. We use a neural network $f$ to map each example from $M$ to a common latent space, where the closest centroid to this embeding gives the class of this sample.

### Prototypical networks.
In the latent space, each class $k$ has a centroid $c_k$. The probability that a given sample $x$ belongs to class $k$ is

$$p(k | x) = \frac{\mathrm{exp} (- d(f(x), f(c_k)))}{\sum_{l=1}^K \mathrm{exp} (- d(f(x), f(c_l)))}$$

They use the Euclidean distance as a function $d$.

The centroids are computed as the point which minimizes the sum of distances to the other points in the class. In the Euclidean case, this is equal to the mean of the coordinates

$$c_k = \frac{1}{|S_k|} \sum_{i=1}^{S_k} f(x_{ki})$$

## Method

### Hierarchical classes

They propose to organise musical instrument classes as nodes wihin a tree with $H$ levels.
Each level $h$ in the hierarchy contains a set of classes $K_h$, such that each parent class comprises multiple child classes and each child class has only one parent class. $T_{ih}$ is the $i$-th class of the $h$-th level.

### Hierarchical prototypical networks

They propose prototypical networks with multiple levels of prototypes organised into a tree (each child prototype belongs to only one parent protoype).

The prototype at of class $i$ at level $h$ is $c_{i,h}$. This is computed as the Euclidean mean of its children prototypes 

$$x_{i,h+1} = \frac{1}{|S_{i,h}|} \sum_{x_{i,h} \in S_{i, h}} f_\theta (x_{i,h})$$
$\{c_{j, h-1} | T_{j, h-1} \subseteq T_{i, h}\}$

Is the representation network the same for every level?

### Hierarchical loss

The loss at every level is the cross-entropy of the softmax

$L() = $


# Review

We expect you to give a report of the **main contribution** of the paper, the **general context** of its discovery and the potential **weak points**, the potential **applications** and **future work** it would allow both in the context of research but also **applied to Apple Music’s context**.

\paragraph{Contributions}

\citet{Garcia2021LeveragingHS} propose a hierarchical prototypical network for few-shot musical instrument recognition: classifying with few training examples the instrument playing in an audio recording. In prototypical networks, the probability that a query sample $\mathbf{x}_q$ belongs to class $k$ depends on the distance between its embedding $f_\theta(\mathbf{x}_q)$ and the ``prototype'' of that class: $\log p(k | \mathbf{x}_q) \propto -||f_\theta(\mathbf{x}_q) - \mathbf{c}_k||^2$. A prototype is the average embedding of the training samples in its class: $\mathbf{c}_k = \frac{1}{|S_k|} \sum_{\mathbf{x}_s \in S_k} f_\theta (\mathbf{x}_s)$.

The proposed model classifies the query sample against a different set of prototypes at each level of a hierarchy, where the parent prototype is the average of its children prototypes. This improves the classification accuracy over a non-hierarchical baseline \citep{Wang2020FewShotDT}, and decreases in mistake severity (the hierarchical distance between the predicted class and the ground-truth). The performance gain is largest for instruments with little data.

\paragraph{Context}

\citet{Sun2019HierarchicalAP} have previously proposed similar hierarchical prototypical networks for few-shot text classification. \citep{Wang2020FewShotDT} performed sound event detection using single-level prototypical networks. \citet{Essid2006HierarchicalCO} trained feature extractors using the hierarchical structure of musical instrument taxonomies.

\paragraph{Weakness}

The F1 score increase $\sim 0.01$ over the baseline \citep{Wang2020FewShotDT} is negligible compared to confidence intervals $\sim0.2$. Besides, adding more levels to the hierarchy decreases the model's performance. This suggests a problem with how the model aggregates prototypes: Because classes with many samples weigh the same as those with few samples, noise from rare classes gets amplified with each level in the hierarchy. A solution could be to weigh each prototype by the number of training samples in its support.

% The hypothesis testing doesn't alleviate these concerns, because it doesn't take into account the variability of scores. Wilcoxon signed-rank is a paired test which shows that, for any given run, the F1 score of the hierarchical model is likely to be higher than the baseline \citep{Fay2010WilcoxonMannWhitneyOT}. The authors should have additionally used an unpaired Mann-Whitney test, which might have revealed that the F1 score difference between the models is insignificant in comparison with the spread of scores for each model.

% Also, there is a mistake in equation 3: $\hat{x}_s$ should not be passed through the representation network $f_\theta$ since it is already a prototype in the latent space.

\paragraph{Relevance}

Few-shot musical instrument recognition is relevant for Apple Music as a lightweight feature extractor in content analysis tasks, such as genre recognition \citep{Tzanetakis2002MusicalGC} or recommendations \citep{Liang2016FactorizationMT}. For these tasks, the proposed method can be extended to recognise multiple instruments at the same time point using multi-label prototypical networks \citep{Lanchantin2017PrototypeMN}.

% Particularly, string distance on temporal musical instrument tags is useful to identify song similarity \citep{Benetos2006MusicalIC}.