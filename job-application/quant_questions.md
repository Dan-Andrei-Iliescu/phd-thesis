# Quant Questions

1. You can roll a 6-sided dice up to 2 times. After the first roll, if you get a number 𝑥, you can decide to either to get 𝑥 dollars or to choose to continue rolling. But once you decide to continue, you forgo the number you just rolled. If you get to the second roll, you’ll just get 𝑥 dollars if the second number is 𝑥 and the game stops. What is the game worth and what is your strategy?

> A. The best strategy is to take the money after 1 time if I win more than the expected value for 1 time. The expected value for 1 time is $3.5$. The expected value for 2 times is $P(X > 3.5) ~ E[X > 3.5] + P(X < 3.5) ~ 3.5 = 4.25$.

**Q. Frequency problem.** Two desk workers receive papers to sign at intervals distributed according to exponentials with parameters $\lambda_1, \lambda_2$ respectively. However, with probability $\pi_1, \pi_2$ respectively, the workers refer the papers to their superior. Both workers have the same superior. What is the expected length of an interval between two successive papers that the superior receives? What is the distribution of that interval?

> A. The pdf of an exponential distribution is $\lambda e^{-\lambda x}$ and its mean is $\frac{1}{\lambda}$.
> 
> We understand that this is a Markov process, that the probability of an interval is independent of the length of the previous interval.
> 
> Assume the boss had just received a paper. $X$ is the time it takes for the boss to receive the next paper. $E[X]$ is what we want to find.
> 
> Assume the boss has just got a paper from worker 1. $E[X|1] = a \frac{\pi_1}{\lambda_1} + b \frac{\pi_2}{2 \lambda_2}$


There are 4 options. The boss could receive both papers from worker 1, both from worker 2, the first from 1 and the second from 2, and the other way around.


What is the probability that the 



$A$ is the time after the last paper at which worker 1 sends his first paper. $B$ is the same for worker 2.

$E[1_A + 1_B]$ is the expected interval length. $E[1_A + 1_B] = E[1_A] + E[1_B]$.

$E[1_A] = P(A < B) E[1_A| A] + P(B < A) E[1_A | B]$ where $E[1_A | A]$ is the expected interval if worker 1 was the last worker and $P(A < B)$ is the probability that 1 was the last worker.

$$P(A < B) = \int P(A < x) P(B = x) dx$$
$$= \int (1 - e^{-\lambda x}) \lambda e^{-\lambda x} dx$$
$$= \int \lambda e^{- \lambda x} dx - \int \lambda e^{-2 \lambda x} dx$$

$$E[1_A | B] = $$

This is a Markov chain with two states: worker 1 and worker 2 


**Q.** The correlation between 3 random variables is the same. What is the range of the value of the correlation?

> **A.** Let us assume that the variance of any of the 3 random variables is 1, such that the correlation is equal to the covariance. The covariance matrix must be positive semidefinite. So $\sum_{i,j}^3 x_i x_j C_{ij} \geq 0, \forall x \in \mathbb{R}^3$. Let us assume that the covariance is the same $C_{ij} = \alpha$ if $i \neq j$ else $1$. So $3 + v \sum_{i \neq j}^3 x_i x_j \geq 0, \forall x \in \mathbb{R}^3$.

>> $\mathrm{var}(\alpha a + \beta b + \gamma c) = \mathrm{var}(\alpha a + \beta b) + \gamma^2 \mathrm{var}(c) + 2 ~ \mathrm{cov}(\alpha a + \beta b, \gamma c) = \alpha^2\mathrm{var}(a) + \beta^2 \mathrm{var}(b) + \gamma^2 \mathrm{var}(c) + 2 \alpha \beta \mathrm{cov} (a,b) + 2 \alpha \gamma \mathrm{cov} (a,c) + 2 \beta \gamma \mathrm{cov} (b,c) = \alpha^2 + \beta^2 + \gamma^2 + 2v (\alpha \beta + \alpha \gamma + \beta \gamma) \geq 0$. So, $v \leq \frac{\alpha^2 + \beta^2 + \gamma^2}{2 (\alpha \beta + \beta \gamma + \alpha \gamma)}$ if $(\alpha \beta + \beta \gamma + \alpha \gamma) \geq 0$ else 
>>
>>> $\mathrm{cov} (\alpha a + \beta b, \gamma c) = \gamma E[(\alpha a + \beta b) c] - E[\alpha a + \beta b] \gamma E[c] = \alpha \gamma E[ac] + \beta \gamma E[bc] - \gamma (\alpha E[a] + \beta E[b])E[c] = \alpha \gamma \mathrm{cov}(ac) + \beta \gamma \mathrm{cov}(bc)$