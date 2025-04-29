# Group-based Learning of Disentangled Representations with Generalizability for Novel Contents
**Link:** https://api.semanticscholar.org/CorpusID:199466320
**Autor:** Haruo Hosoya
**Subiect:** [[group_instance_disentanglement]]

- Infer separate content and transformation factors from sensory data
- Existing methods are limited because
	- They require explicit labels for some attributes
	- They do not allow for generalisation over novel contents
- Their Group-based VAE allows for
	- Transformation invariance
	- Content generalizability
- Content transformation separation problem [[Separating Style and Content with Bilinear Models]]
	- The most typical approach (semi-supervised) learns a generative model by explicitly supplying class labels to the content variable while extracting the remaining factor in the transformation variable [[Semi-supervised Learning with Deep Generative Models]] [[Discovering Hidden Factors of Variation in Deep Networks]] [[Learning Disentangled Representations with Semi-Supervised Deep Generative Models]]
	- Other approaches use a more sophisticated method, such as adversarial learning, that exploits labels so as to make the content representation as irrelevant as possible to transformation [Wang __et al.__, 2017; Lample __et al.__, 2017; Mathieu __et al.__, 2016]. Although these approaches can potentially allow for generalization over new contents, their requirements of specific kinds of label are often difficult to fulfill, e.g., attribute labels corresponding to transformation.
	- Concurrently with ours, one recent study has developed another group-based method called [[bouchacourt_2018]]. In this, they adopt a sophisticated technique called “evidence accumulation” for estimating the group-common factor. However, as we show later, this particular technique has an unfortunate property that the learned content representation often becomes dependent on the transformation, which potentially conflicts the goal of disentangling
- ![[2021-09-08-01.png]]
- They first estimate each instance variable, then build the group variable.