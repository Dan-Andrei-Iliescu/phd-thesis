# Advances and Open Problems in Federated Learning

[Semantic Scholar](https://api.semanticscholar.org/CorpusID:209202606)

## Non-IID Data in Federated Learning
- Non-IID data has a close mapping to notions of dataset shift.
- Supervised federated learning involves firs drawing a client $e \sim \mathcal{Q}$ and then a data pair from that client $(x, y) \sim \mathcal{P}_e(x, y)$
  - The distributions $\mathcal{Q, P}$ may change over time.
  - Even within a single client content might not be i.i.d (e.g. consecutive frames in a video). *The solution to this is shuffling.*

**Non-Identical Client Distributions** Using the product rule on the joint probability $P(x, y) = P(y|x) P(x) = P(x | y) P(y)$ allows us to identify multiple ways in which the data distribution can be different across clients:
1. **Covariate Shift:** $P(x)$ changes, $P(y | x)$ stays the same. **e.g.** x is the client location, y is the chance that it snows. For the same location in different clients the chance that it snows is the same. *In principle, training a global model here is appropriate.*
2. **Label Skew:** $P(y)$ changes, $P(x | y)$ stays the same. **e.g.** y is the animal species, x is the image. Some animals live only in certain places.
3. **Concept Drift:** $P(x | y)$ changes, $P(y)$ stays the same. **e.g.** Handwriting recognition, y is the letter, x is the image. The distribution of letters is the same, but some people use the same strokes for different letters.
4. **Concept Shift:** $P(y | x)$ changes, $P(x)$ stays the same. **e.g.** x is the image, y is whether the client thinks the image is beautiful or ugly. This is a matter of personal preference.
5. **Quantity Skew:** One client has vastly more data than another client.

## Personalization
Sometimes, the clients are so different that separate models trained on individual clients might perform better than global models trained on all of the data. There are multiple ways to personalize a global model:
1. **Feautrization:** Add features to the global model reflecting the particular case of a client
2. **Multi-Task Learning:** Each client (or subset of clients clustered by some criterion) is a task, and we learn a global model to perform multiple tasks.
3. **Model Agnostic Meta-Learning:** We first sample a task and then sample the data.

*They don't mention what happens if we want to generalize to a new client!*