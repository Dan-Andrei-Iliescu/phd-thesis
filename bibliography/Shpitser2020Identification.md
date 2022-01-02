# Identification and estimation in graphical models of missing data

[Youtube Talk](https://www.youtube.com/watch?v=FRYkkQBfrDg)

Missing data as a causal (counterfactual) problem. $X_i^{(1)}$ is the true variable, $X_i$ is the observed proxy and $R_i$ is the missingness variable.

$$X_i = \begin{cases} X_i^{(1)}, ~~ R_i = 1 \\ ?, ~~ R_i = 0 \end{cases}$$

In this formulation $X_i^{(1)}$ is the counterfactual: "What would $X_i$ have been if $R_i$ had been 1?"

Missingness data models can be viewed as factorizations of the joint data distribution with respect to a directed acyclic graph. If $O$ is the observed variables, then the factorization takes the form $p(O, X, X^{(1)}, R) = p(X^{(1)} | X, R) ~ p(X, O, R)$.