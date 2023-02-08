# Quant Primer

## Old friends

### Air force one

**Q.** One hundred people are in line to board a plane which has exactly 100 seats. Each passenger has a ticket assigning them to a specific seat, and the passengers board one at a time. The first person to board is drunk, picks a random seat, and sits in it. The remaining passengers board; if they find their assigned seat empty, they sit in it. If they find their seat taken, they pick a random seat to sit in. Everyone boards, and is seated. What is the probability that the final person who boards gets to sit in their assigned seat?

**A.** The first person can sit in either their own seat, making the last person sit in their own seat, sit in seat 100, guaranteeing that the last person won't seat in their own seat, or sit somewhere else, allowing another person to sit in seat 100 by accident. 

If option 3, then the problem repeats when the person with that number boards the plane. At that point, the only seats left will be seat 1 and the seats with a greater number. So if the drunk passenger sits in seat 40, passenger 40 will have available 61 seats to choose from. Then the expected value of passenger 100 sitting in their seat will be $E_{61}$.

$E_n$ is the probability that passenger 100 will sit in their seat if passenger $101-n$ will sit in a random seat (either the first passenger or some passenger whose seat is full).

$$E_{n} = \frac{1}{n} + \frac{1}{n} \sum_{i=2}^{n-1} E_i, ~ E_2 = \frac{1}{2}$$

$$E_3 = \frac{1}{3} + \frac{1}{3} \frac{1}{2} = \frac{1}{2}$$

$$E_4 = \frac{1}{4} + \frac{1}{4} E_3 + \frac{1}{4} E_2 = \frac{1}{2}$$

So I think the answer is $\frac{1}{2}$ but I don't know why. We might be able to solve this with symmetry.

Proof by induction: If we assume $\{E_2, \dots E_{n-1}\}$ are all 0.5, then $E_n$ is also 0.5.

$$E_n = \frac{1}{n} + \frac{1}{n} \sum_{i=2}^{n-1} E_i = \frac{1}{n}  + \frac{1}{n} (n-2) \frac{1}{2} = \frac{n}{2n} = \frac{1}{2}$$



## Soft interview

### Their questions

- Can you walk me through your CV? This is common, and is usually asked at the start of a
phone interview. Rehearse an answer and try to keep it shorter than three minutes. It is
vital to prepare a response and to tell it like a story. It looks bad if you can’t articulate the
contents of your CV.
    - I'm doing a PhD in Machine Learning at the University of Cambridge. I'm developing ML algorithms to learn from heterogeneous data (data from multiple environments) and data with missing values. I've written a paper on generative models for grouped data that I evaluated on abstract reasoning tasks. I've also built a software for visualising urban transport data using Pandas as a backend.
    - I'm doing an internship with Papercup, a company using AI to dub videos in different languages. I'm developing there a deep learning model for time-series that can fill in missing values. I am applying it to speech audio, but also climate modelling.
    - I'm teaching Data Science (Bayesian and frequentist statistics, markov chains) and Machine Learning and Bayesian Inference (Gaussian Processes, Expectation Maximisation, Markov-Chain Monte Carlo).
- Why are you looking for a new job? I once had a phone interview where, upon answering the call, the guy immediately blurted “Hi OK tell me why you want to leave your current job for one in finance?” He didn’t even pause to tell me his name. You should have your answer to this question so well rehearsed that it sounds completely natural.
    - I am finishing my PhD and would like to move into industry.
- Why do you want to work in finance?
  - I've always been a bit fascinated with markets and the history of economics. However, since the war in Ukraine and the supply-side crisis post-covid I became fascinated with how asset prices fluctuate in the market.
- Why do you want to work for this firm and not our competitor?
  - I became aware of GSA Capital with a competition, called GSA Spark. I then saw a talk last week that Julian Roth gave in Cambridge, talking about how GSA capital stays competitive. I was interested in how GSA capital was using alternative data to build more powerful models.
- Can you take me through one of your research projects? What is the difficult part?
  - The project I'm working on in Papercup at the moment is interesting. We are trying to offer users a way to modify the prosody of generated speech, without requiring them to do labour-intensive work. My model is a transformer that takes as input multiple streams of missing data provided by the user and outputs a full stream of generated audio.
  - The difficult part of the problem is how to encode data from different modalities, of different kinds. I had the idea to use learned positional embeddings, basically a separate learned parameter for each kind of data that would map all the data types in a common latent space.

### My questions

- What position would I be considered for?
- What kind of research is going on at the moment?
- What are you developing that's most exciting at the moment?
- What is the ratio of the different parts of quant finance: data processing, ML models, statistics, finance, trading? Which do you spend most time on day to day?


## Coding interview 1

### Question 12

**Q.** You have two urns, $N$ red balls, and $N$ blue balls. You can distribute the balls into the urns any way you like, but each urn must have at least one ball in it. I will choose one urn at random (p = 0.5) and then draw one ball from it. If the ball is blue, you win. How should you distribute the balls to maximise your probability of winning? Log into this pair-programming website and
use Python or C++ to solve the problem while I watch.

**A.** I want to maximise the probability of winning in terms of the urn assigned to each ball, which is 
$$P = p \frac{b}{b + r} + (1 - p) \frac{N - b}{2N - (b + r)}$$

Also, $b, r \in \{1:N-1\}$.

