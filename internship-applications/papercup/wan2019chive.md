# CHiVE: Varying Prosody in Speech Synthesis with a Linguistically Driven Dynamic Hierarchical Conditional Variational Network

## Abstract

Training text-to-speech by conditioning only on the text produces a flat prosody because it averages over all the variation in prosody in the dataset. In order to sample diverse prosody, they introduce a conditional variational autoencoder (conditional on what?). A prosody can be sampled from the variational layer, then decoded into something which can be turned into a waveform using wavenet. The encoder and decoder have a hierarchical structure, with a level for words, syllables, and phonemes. This hierarchical model outperforms a flat state-of-the-art baseline. Additionally, their model can perform translation of a text to a prosody sampled from another speech signal.


## Introduction

- Conventional prosody prediction techniques assume there is a one-to-one mapping between text and speech, which there isn't. This reminds me of how in Ctrl-P the acoustic feature predictor provides one single prediction for a given text.
- In these methods, F0 is modelled independently from duration, which is a problem
- Because these methods are phoneme- or frame-based, they don't produce prosody profiles compatible with linguistic speech patterns

They use CVAE by Sohn, which conditions both the encoder and the decoder.

The encoder takes as input linguistic features (part-of-speech, syllable and phoneme attributes) and prosodic features (F0, energy and duration). The linguistic features are fed to the decoder as well. Both enc and dec are hierarchical, and one important aspect is that the unrolled length of each level is different, depending on the input. For example, a word could contain more or fewer syllables. This is why this is called dynamic.

There are 2 ways to run the model at inference time. The first is to sample the latent vector and generate realistic prosodies (with 0 representing the average prosody). The second is to use the encoder, but change the linguistic features from the encoder to the decoder.

## Model

The model is a CVAE where the prosodic features are reconstructed and the language features are the conditioning. The language features are at multiple levels: frame, phoneme, syllable, word, sentence. The prosodic features are at two levels: F0 and c0 for frames, duration for phoeneme. The task is to reconstruct these features.

In the encoder, there are 3 RNNs: frame-rate, phoneme-rate and syllable rate. The features of the frame-rate are F0, c0 and linguistic features (what are they?). The features of the phoneme-rate are duration and linguistic features. The context vector of the RNN is extracted at the end of every syllable (hard-coded) and used as feature for the syllable-rate. The syllable-rate additionally receives as input syllable-, word-, and sentence-level features which are carried-forward.

## Evaluation

### Naturalness against baseline

They compare with an equivalent model to CHIVE but which doesn't have the dynamic component. The LSTM runs at the frame-level, which is then broadcast at higher level (how?). They ask people to rate the speech produced by randomly sampling prosody representations for pairs of text. The results are okay-ish, 45% vs 25%. 

They used a binomial test, is that appropriate? The p-value measures what is the probability that you get more than 46% of comparisons to go CHIVE if you assume the probability of preferring CHIVE is 0.5.

### Variation of a single utterance

They produce speech signals for the same utterance by varying the prosody representation. Firstly, they show that the speech produced by the encoded prosody embedding is close in its F0 profile to the ground-truth. Secondly, the speech produced with the 0 prosody embedding is close the baseline. Thirdly, speech produced by sampling embeddings have a diverse F0 profile.

### Prosody error

They measure the prosodic attributes of the output and compare it to the ground-truth. This is the error. They compare the error between CHIVE and baseline, and between random samples, 0 vector and encoded representation. CHIVE works better than baseline and encoded > 0 > random. The differences are smaller between models than they are between regimens.

### Prosody transfer

The linguistic features of a sentence are decoded with the prosodic features of another. We see that the F0 curves change, which means some transfer is taking place. But there is no measure of how natural or appropriate the transfer is.