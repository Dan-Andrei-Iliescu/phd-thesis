# Math for Quantitative Finance


- A log-normal distribution is the standard model for a stock.
- A good model will make the stock move in proportion to its size.
- Default is rare, but default events across houses are correlated.
- What we are interested in usually is not expected value but expected utility.


> **Q.** A stock can either rise or fall according to the following Markov Chain transition probabilities.
> $$P = \begin{bmatrix} 0.8 & 0.2 \\ 0.4 & 0.6\end{bmatrix}$$
> What is the marginal probability that the stock will rise?
> 
> **A.** The probability distribution over states $\pi$ is stable if, after sampling a random state from $\pi$ and following a random transition according to $P$, the expected value of the indicator variable will be equal to $\pi$.
> $$\pi = 0.8 ~ \pi + 0.4 ~ (1 - \pi)$$
> $$\pi = \frac{2}{3}$$

## Probabilities
- Use symmetry when no outcome is more likely than another.
- The probability that $n+1$ coin flips has more heads than $n$ coin flips is always $1/2$!

> **Q.** The probability that at least one company is going to announce a takeover in the next hour is 84%. What is the probability that at least one announces in the next 30 minutes?
> 
> You may assume that if $I_1$​ and $I_2$​ are two non-overlapping time intervals, the probability of no announcement in $I_1$​ is independent of the probability of no announcement in $I_2$​.
> 
> **A.** $X$ is the time (in hours) when the first takeover is announced, such that $P(X < 1) = 0.84$.
> $$P(X < 1) = P(X < s) + (1 - P(X < s)) ~ P(X < 1 - s)$$
> When $s=0.5$
> $$P(X < 0.5)^2 - 2 ~ P(X < 0.5) + 0.84 = 0$$
> $$P(X < 0.5) = 0.6$$

**Principle of inclusion-exclusion.** $P(A \cup B) = P(A) + P(B) - P(A \cap B)$

### Conditional probabilities

> **Q.** You have a jar with 4 fair coins and 1 unfair coin (which has heads on both sides). You choose one of the 5 coins at random, flip it 5 times, and get all heads. What is the probability that you chose the unfair coin?
> 
> **A.** 
> $$P(U | F) = \frac{P(F | U) P(U)}{P(F)}$$
> $$P(F | U) = 1, ~ P(U) = \frac{1}{5}, ~ P(F) = \frac{1}{5} + \frac{4}{5} \frac{1}{2^5} = \frac{9}{40}$$
> $$P(F | U) = \frac{8}{9}$$


### Interview - Probability

> **Q1.** A $3 \times 3 \times 3$ cube is painted red, and then cut into $27$ $1 \times 1 \times 1$ cubes. One of these cubes is chosen at random, and rolled like a die. What is the probability that it lands with a painted side facing up?
> 
> **A.** There are 8 cubes with 3 painted faces, 12 cubes with 2 painted faces, 6 cubes with 1 painted face, and 1 cube with no painted faces. There are 27 cubes in total
> $$P = \frac{8}{27} \frac{3}{6} + \frac{12}{27} \frac{2}{6} + \frac{6}{27} \frac{1}{6} = \frac{54}{162} = \frac{1}{3}$$

> **Q2.** There are two boxes, each with three balls. Box A has two red balls and one blue ball; Box B has one red ball and two blue balls. I randomly choose a box, and randomly draw a red ball. If I then draw another ball from the same box, what is the probability that it is also red?
> 
> **A.** $P(Y|X) = \frac{P(X,Y)}{P(X)}$, where $P(X,Y) = \frac{1}{6}$ and $P(X) = \frac{1}{2}$, so $P(Y|X) = \frac{1}{3}$.


## Expected Value

- **Linearity of expectation.** $E[X+Y] = E[X] + E[Y]$ even when $X,Y$ are dependent!
- **Indicator variable.** $P(X \in S) = E[1_{X \in S}]$.

> **Q.** The price of Stock A in one month is (approximately) normally distributed with mean $100 and standard deviation $25. The price of Stock B in one month is (approximately) normally distributed with mean $50 and standard deviation $5. They have a correlation of 90%. If you buy 3 shares of stock A and (short) sell two shares of stock B, what is the expected value of your portfolio (assuming these actions are all it contains) in one month (in dollars)?
> 
> **A.** $E[3 A - 2 B] = 3 E[A] - 2 E[B] = 200$ where $E[A] = 100, E[B] = 50$.

> **Q.** You flip 10 coins and are paid $1 for each consecutive pair of heads. For example, if you flipped TTHHHTHHTT, you would be paid $3. What is the expected value of this game in dollars?
> 
> **A.** $E[\mathbf{1}_{X_1 = H, X_2 = H} + \dots + \mathbf{1}_{X_9 = H, X_{10} = H}] = E[\mathbf{1}_{X_1 = H, X_2 = H}] + \dots + E[\mathbf{1}_{X_9 = H, X_{10} = H}] = 9 \frac{1}{4} = 2.25$. 

> **Q.** A work event gets very rowdy, and no one can remember which coat they brought. So each person takes a random coat as they leave. If each of the 100 employees brought exactly one coat, what is the expected number of people who get their correct coat?
> 
> **A.** $E[1_1 + \dots + 1_{100}] = 100 ~ E[1_i] = 1$.  

### Expected Utility

- People will maximise their expected utility, not their total wealth. This known as charging for risk.
- Usually the argument of the utility is the total amount that I have, not the difference.

> **Q.** A trader is presented with the following game as a one-time offer, with a set starting amount the trader must pay in to play: A fair coin will be flipped until a heads appears, and you will be paid  $\$2^n$ if there are n flips. 
> 
> If her manager tells her to optimize the utility function U(w)=w with an initial wealth of $100, what is the most she would pay to play this game? 
> 
> Assume, unrealistically, that there is no counterparty risk; i.e., the person offering this game can actually pay out any sum of money.
> 
> **A.** $E[w] = 2 \frac{1}{2} (1 + E[w]) = \infty$. Therefore, you should give all the money you have.

> **Q.** Once again, a trader is presented with the following game as a one-time offer: A fair coin will be flipped until a heads appears, and you will be paid  $\$2^n$ if there are n flips. This time, her manager tells her to optimize the utility function $U(w)=\log_e (w)$ with an initial wealth of $100.
> 
> **A.** We want to find the cost of the game $C$, such that the expected utility of playing the game $E_W[U(100 - C + W)]$ to be equal to the utility of not playing the game $\log_e 100$. The expected utility of playing the game is $E = \frac{1}{2} (\log_e (102 - C) + \log_e (100 - C + 2E))$. Therefore, we are looking for the value of $C$ that solves $\log_e 100 = \frac{1}{2} (\log_e (102 - C) + \log_e (100 - C + 2 \log_e 100))$. The value is $C \approx 6$.

### Interview - Expectation
> **Q.** Every second, an ant chooses one of the (unoccupied) vertices of a tetrahedron and moves there. What is the expected number of seconds until it has visited every vertex?
> 
> **A.** Let $R_i$ be the number of seconds between visiting the $(i-1)$-th and the $i$-th vertex. $X = R_1 + R_2 + R_3 \implies E[X] = \sum_{i=1}^3 E[R_i]$. $R_i$ are not identical, however. $R_1 = 1, R_2 = \frac{3}{2}, R_3 = 3, R_i = \frac{3}{4-i}$. So $X = 5.5$.

Expected value isn't reversible; e.g., the expected number of vertices after $n$ seconds won't give us the expected number of seconds needed to visit $n$ vertices.

## Sharpe Ratio

It measures how much excess return you get for the extra volatility of holding a risky asset. It represents the additional amount of return that you get for a unit of risk.

If $R$ is a random variable modelling the return on our investment, and $R_f$ is a random variable modelling the return of a risk-free investment, then the Sharpe Ratio is:

$$S(R) = \frac{\mathrm{E}[R - R_f]}{\sqrt{\mathrm{var} [R - R_f]}}$$

## Variance

$$\mathrm{var}[X] = E [X - E[X]] = E[X^2] - (E[X])^2$$

Variance is kind-of distributive:

$$\mathrm{var}[nX] = n^2 \mathrm{var}[X]$$

The variance of the sum of independent r.v. is additive:
$$\mathrm{var}[X + Y] = \mathrm{var}[X] + \mathrm{var}[Y]$$

Variance is invariant to relocations:

$$\mathrm{var}[X + n] = \mathrm{var}[X]$$

The variance of a multi-branched process is not the average of the variances fo the branches.

### Covariance

$$\mathrm{cov} [X, Y] = E[(X - E[X])(Y - E[Y])] = E[XY] - E[X]E[Y]$$

This is how to find the variance of the sum of two dependent RVs:

$$\mathrm{var} [X + Y] = \mathrm{var} [X] + \mathrm{var} [Y] + 2 \mathrm{cov} [X, Y]$$

> **Q.** Every day, the price of a stock increases with probability $\frac{1}{3}$ and decreases with probability $\frac{2}{3}$. Let U be the number of days it goes up, and D be the number of days it goes down, over the course of a 10-day period. What is cov(U,D) cov(U,D)?
> 
> **A.** $\mathrm{cov} [U, D] = \frac{1}{2} (\mathrm{var} [U + D] - \mathrm{var} [U] - \mathrm{var} [D])$. $\mathrm{var} [U + D] = \mathrm{var} [10] = 0$. $\mathrm{var} [U] = np(1-p) = 10 \frac{2}{9}$, same for $D$. So, $\mathrm{cov} [U, D] = - \frac{20}{9}$.

Correlation is

$$\rho_{X, Y} = \frac{\mathrm{cov} [X, Y]}{\sigma_X \sigma_Y}$$

Variance of a binomial variable is $np(1-p)$.

The variance of a sum of dependent random variables is

$$\mathrm{var} \left[ \sum_{i=1}^n X_i \right] = \sum_{i=1}^n \mathrm{var} [X_i] + \sum_{i,j=1}^n \mathrm{cov} [X_i, X_j]$$

### Interview - Variance

> **Q.** You are playing a game in which you will be paid $1 for each pair of consecutive heads you flip out of 10 coins. For example, if you flip THHHTTHHTT, you will receive $3. What is the variance of your payout?
> 
> **A.** Let $X_i$ denote if throws $(i, i+1)$ are both heads or not. The result we are looking for is $\mathrm{var} \left[ \sum_{i=1}^9 X_i \right] = \sum_{i=1}^9 \mathrm{var} [X_i] + \sum_{i,j=1}^9 \mathrm{cov} [X_i, X_j]$. We know that $\mathrm{var} [X_i] = \frac{3}{16}$. We know that $\mathrm{cov} [X_i, X_j] = 0$ when $j \neq i + 1$ or vice-versa. So $\sum_{i,j=1}^9 \mathrm{cov} [X_i, X_j] = 16 \mathrm{cov} [X_i, X_{i+1}]$. And $\mathrm{cov} [X_i, X_{i+1}] = E[X_i X_{i+1}] - E[X_i]E[X_{i+1}] = \frac{1}{8} - \frac{1}{4} \frac{1}{4} = \frac{1}{16}$. Sooo, $\mathrm{var} \left[ \sum_{i=1}^9 X_i \right] = 9 \frac{3}{16} + 1 = \frac{43}{16}$.