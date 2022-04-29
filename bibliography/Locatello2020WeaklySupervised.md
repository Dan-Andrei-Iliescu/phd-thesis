# Weakly-Supervised Disentanglement Without Compromises

*The goal of disentangled representation learning is to learn a function r(x) mapping
the observations to a low-dimensional vector that contains all the information about each factor of variation, with each coordinate (or a subset of coordinates) containing information about only one factor.*

*State-of-the-art weakly-supervised disentanglement
methods (Bouchacourt et al., 2018; Hosoya, 2019; Shu et al.,
2020) assume that observations belong to annotated groups
where two things are known at training time: (i) the relation
between images in the same group, and (ii) the group each
image belongs to.*


*On the other hand, many data modalities are not observed
as i.i.d. samples from a distribution (Dayan, 1993; Storck
et al., 1995; Hochreiter & Schmidhuber, 1999; Bengio
et al., 2013; Peters et al., 2017; Thomas et al., 2017;
Schölkopf, 2019).*

## My summary of introduction
Disentanglement is the goal of learning representations which separate between the independent factors of variation in the data. This is useful because of certain properties like interpretability, predictive performance, abstract reasoning etc.

However, Locatello has discovered that it is theoretically impossible to disentangle from i.i.d. samples. In practice, learning is unstable and dependent on spurious things.

Moreover, many data modalities do not present themselves as i.i.d. samples (like time series, actions, grouped images etc). There, observations are related to one another by tiny shifts in the factors of variation.

Therefore, state-of-the-art weakly-supervised learning methods learn disentangled representations based on groups within which observations are related in some way.

However, real life problems rarely present neatly packed groups. More often, pairs of datapoints are related in an unstructured way, with the caveat that no two datapoints vary in too many factors of variation.

Therefore, we propose a method for learning disentangled representations for this setting.