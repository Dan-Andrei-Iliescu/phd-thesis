# Literature review

## Unsupervised Speech Decomposition via Triple Information Bottleneck

[Qian2021Unsupervised](https://arxiv.org/pdf/2004.11284.pdf) propose a system that can disentangle all 4 aspects of speech (timbre, pitch, rhythm and content) without the use of any text labels. Previous speech-synthesis systems could only separate timbre.

Disentanglement is used in speech-analysis tasks to remove nuisance factors. It is also foundational to generation tasks such as voice conversion, emotional speech, prosody modification and low bit-rate synthesis.

They propose an autoencoder based method where the speaker identity is provided as an explicit label, and separate encoders learn the other 3 features. In order to separate between them, the rhythm encoder and the content encoder receive the full spectrogram, while the pitch encoder receives the pitch contour. The pitch and content encoders have their imput time-warped in such a way that the rhythm information is contaminated. The method relies on the assumption that each encoder will learn what the other encoders can't provide. They also assume that each encoder will learn only this, since an information bottleneck is applied to them (takes the form of restricting the number of units).

## Temporal control of prosodic variation for speech synthesis

[Mohan2021CtrlP](https://arxiv.org/pdf/2106.08352.pdf)

There are multiple ways in which the same text can be translated to speech. We don't want to average out all options, because no one speaks like that. One approach is to capture the variability in speech using a latent representation. However, this leads to undesirable artifacts in the generated speech.

They propose an alternative where they control prosody by conditioned on the acoustic features F0, energy and duration, which are related to prosody. They use a modified Tacotron-2 enc-dec model where the encoder outputs are concatenated with the estimated acoustic features. During training, the acoustic features are estimated from force-aligned data (text aligned with audio). During testing, the model proposes a default option for those features (estimated from text?) leaving the user to decide which one to modify and how.

Their model achieves good acoustic control with temporal precision (the changes can be applied per-phone and the effects can be seen in a local area). Traditional methods used regression trees to map paralinguistic features to the parameters of the acoustic generative models.

Some works treat the variation in prosody as residual variation which they capture using a latent variable. The latent variables are uninterpretable and entangled, and the generated speech sometimes produces artifacts. In contrast, the proposed model conditions directly on estimated acoustic features. Methods which condition on extracted acoustic features either have one value for the whole audio recording or require annotations per-frame, both of which are not suitable for human-in-the-loop control.

The proposed method is a modification of the Tacotron-2 encoder-decoder with multi-speaker (can condition on the speaker?). The produced mel-spectrogram is converted into a waveform by a pre-trained WaveRNN.

- $\{p_1, \dots p_N\}$ are the phones to be synthesised
- $\{y_1, \dots y_T\}$ are the frames of the ground-truth mel spectrogram
- $\{a_1, \dots a_N\}$ are the extracted acoustic features. These are 3-dimensional.
- $\{e_1,\dots e_N\}$ are the decoder outputs.

> [Mel Spectrogram](https://medium.com/analytics-vidhya/understanding-the-mel-spectrogram-fca2afa2ce53) take the fourier transform per window and then transform through a log scale.

At inference, the acoustic features $a$ are predicted from the encoder outputs $e$ using an LSTM.

# Thoughts

Infer a controllable latent representation for prosody variation by conditioning the inference of the latent levers on the whole audio sequence

The latent representations will be inferred conditionally on the extracted features and on the embedding of the whole audio sequence.

Conditioning the latent representation has the potential to increase disentanglement and expressivity, according to [Khemakhem2020Variational](https://proceedings.mlr.press/v108/khemakhem20a.html).

Conditioning on the entire sequence allows for more precise estimation of the latent factors, as it removes the speaker-specific residual. I have written a paper on this subject, which is currently under review at ICML, showing that the individual latent representations of observations belonging to a group are inferred more accurately when the encoder is conditioned on the entire group. Previously, this phenomenon has been demonstrated in linear hierarchical models .

My PhD research leads me to believe that conditioning the encoder of a phone on a global representation of the entire sequence will lead to a more accurate inference of the latent representation of a phone. I have a paper under review at ICML showing that a large proportion of the residual of a latent representation of an observation which belongs to a group is actually group-specific, and that by conditioning on a latent representation of that group, the estimate is more accurate.

How about semi-supervised learning? Some ground-truth features might be missing some of the time, like F0, energy, duration, style, speaker identity. Ctrl-P tries to predict defaults from the text, but isn't this too restrictive? What could go wrong? Maybe frames which are close together will have widely different defaults. Unlikely, because they are synthesised by an LSTM so they take context information as input. Also, you would like to have options for these defaults. Sampling the prior would allow you to get those options.

In my PhD I study disentanglement in hierarchical generative models. I've applied them to image-to-image translation (rotating 3D objects, font translation), style-content disentanglement (separating between local and global features of images), missing value imputation for repeated measurements in education, medical and climate data. I discovered that by conditioning an instance-level encoder on the previously inferred group-level representation, the instance representation is more accurate.

For my MPhil I created an adversarial network that can extract a conditional distribution from the joint distribution of the inputs in a VAE.

T-VAE learns latent representations for speaker and style features. One method even has a separate latent variable for unobserved features.

You can have

Learned autoregressive priors for controlling prosody with missing ground-truth features.

Ctrl-P proposes an Acoustic Feature Predictor network to 

Instead of having a network produce acoustic features, it's better to have the network produce latent representations and use conditioning on the acoustic features as an extra training signal. The training signal is present for some frames and absent from others, so the present ones are aggregated using a DeepSets network where each feature is concatenated with a one-hot encoding of the feature identity, then passed through an attention mechanism. The one-hot encoding replaces the positional embedding. This is equivalent to performing a Bayesian update.

> **IDEA:** Deal with missing features by Bayesian updates using the equation that I deduced earlier.

What advantages would this have? Sampling from the prior distribution over the latent rather than 

The problem with controllable models is that you have to provide good default values for acoustic features when you do not want to specify them. It is difficult to produce good default values for the F0, energy and duration using a recurrent network, especially since the features are entangled. The performance bottleneck of the Ctrl-P model is the acoustic feature predictor (AFP). I suspect it finds it difficult

We propose to combine latent representations with explicit features. We propose an autoregressive latent representation which can be variably conditioned on all, some or none of the acoustic features, depending on which ones are present.

An LSTM takes as input the previous context vector, the encoding

Using the notation of Ctrl-P, we compute the new prosody representation as $\pi_i = \mathrm{LSTM} (\pi_{i-1}, \mathbf{e}_i, \mathbf{f}_i)$ where $\mathbf{a}_i = \{(a^{(1)}_i, \mathbb{I}_1), \dots (a^{(F)}_i, \mathbb{I}_F)\}$ is the set of known acoustic features for phone $i$. Let there be $F$ acoustic features in total, but any number of them (including all of them) might be missing for any phone.


$\pi_i = \mathrm{LSTM} (\mathbf{h}_{i-1}, \pi_{i-1}, \mathbf{e}_i, \mathbf{f}_i)$

$\mathbf{f}_i = \mathrm{Attn} (\mathbf{A}_i, \mathbf{h}_{i-1})$

$\mathbf{A}_i = \{(\mathbf{a}^{(1)}_i, \mathbb{I}_1), \dots (\mathbf{a}^{(F)}_i, \mathbb{I}_F)\}$

This enables the introduction of other kinds of features during training that only appear at certain instances in time, such as a labelled change in emotion, or also global features, like style and speaker identity.

Prosody control with missing acoustic features.

The triple information bottleneck uses heuristic data augmentation techniques in order to learn 4 separate representations for each frame in a sequence.


# Structured

## Prosody control when acoustic features are missing

**What am I proposing?** I propose using a latent representation, separate from the outputs of the text encoder, to capture the variation in prosody. The representation is computed autoregressively and can be conditioned on zero, one, or more acoustic features, subject to their availability.

**What is the problem?** We are tying to generate speech from text by controlling the rendition of the speech, the prosody. Some methods try to capture this variation in a latent representation which can then be sampled using a prior distribution. However, this approach offers little control over the values that we want those prosodic features to take, the representation is free to organise its space in a different way than is interpretable for people. Another approach is to condition the decoder on ground-truth acoustic features. This is much more intuitive and controllable for people. However, when acoustic features are not present, a network has to be trained to predict them from the text embeddings. As seen in the paper, there is a large gap between the subjective naturalness of the predicted acoustic features and those adjusted by a human in the loop. This suggests there is space for improvement. 

It is also unclear in the paper if the acoustic feature predictor can modify its prediction for subsequent timesteps if the user adjusts the level of an acoustic feature at a previous timestep.

**How will it work?**

**How is what I am proposing helping?** A latent variable has an advantage over using extracted features because the prior distribution of the latent variable is known and can be sampled. The distribution of the extracted features is more difficult to estimate because it requires a sophisticated function for which there is little data. It is also difficult because this distribution is probably highly multimodal. 

A better approach is to have a latent variable with a simple prior distribution that can be conditioned on the additional acoustic features. This is different from T-VAE because 1) they did not use acoustic features and 2) they use simple conditioning.

Additionally, I propose a new way to accumulate information that allows for different missing features for each phone. Other TTS methods use separate latent variables for present and absent features. Other machine learning methods for conditioning on missing features use semi-supervised learning (replacing the missing feature with a prior distribution) or default values with masks. Our way uses an attention mechanism not on a sequence, but on the set of features. The positional encoding is a one-hot encoding of which feature we are accumulating. This allows for aggregating information over different sets of features depending on which ones are missing. This is used in multiple instance learning.

**How does my experience help with this?** I have worked on accumulating evidence from multiple instances in a group of observations. I have also developed this algorithm for missing data imputation where different features are missing for different datapoints. This algorithm resembles the one proposed above, because each feature is concatenated with a one-hot encoding and passed through an attention mechanism. This is something I am currently researching in my PhD.

**What are the challenges?** 
- It is unclear what prior to use, whether it will be expressive enough?
- Maybe there are other features that can be included in the conditioning, like sound events,emotions.

**What are the next steps?**



