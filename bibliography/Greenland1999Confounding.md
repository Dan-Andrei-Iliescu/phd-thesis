# Confounding and Collapsibility in Causal Inference

Usually three separate concepts are called confounding:
1. A bias coming from the mixing of extraneous factors into the effect of interest.
2. Non-collapsibility.
3. The inseparability of the main effects, also called aliasing.

## Counterfactual view of causality

> *We may define a cause to be an object, followed by another,where, if the first object had not been, the second had never existed* - Hume

**Potential outcomes:** The causal effect of a treatment is a contrast in outcome of the treatment over different patients. This requires identical patients.

## Confounding
- **Treatment:** Agent administered by the experimentor.
- **Exposure:** Agent not controllable.

The setting is that we want to contrast the distribution $p_A(y|x_0)$ with $p_A(y | x_1)$ where $y$ is the outcome, $x_0, x_1$ are treatments and $A$ is the *target population* on which we are testing, the target population. Since we can only apply one treatment to population $A$, we have to apply treatment $x_0$ to a *control population* $B$, and hope that $p_A(y | x_0) = p_B (y | x_1)$. We say that *confounding* happens when this hope is false. Suppose $\mu_{A0}$ is a statistic of $p_A (y | x_0)$. We say an association parameter $\mu_{A1} - \mu_{B0}$ is confounded for a causal parameter $\mu_{A1} - \mu_{A0}$.

Implications:
- Confounding depends on the parameter $\mu$. For example, the difference in 5-year survival rate is different, so that parameter is confounded, but the difference in 10-year survival rate might be the same. Obviously, the difference in 200-year survival rate is 0, since no one lives 200 years, so that parameter is not confounded.
- The same measure of association $\mu_{A1} - \mu_{B0}$ might be confounded for neither, one, or both of $A$ and $B$. For example, $\mu_{A1} - \mu_{B0} \neq \mu_{A1} - \mu_{A0}$ but $\mu_{A1} - \mu_{B0} \neq \mu_{B1} - \mu_{B0}$.
- Absence of confounding $\mu_{A0} = \mu_{B0}$ is not sufficient to identify the *sharp null-hypothesis* that $y_{i0} = y_{i1}$ for every unit $i$ in population $A$.

A covariate difference between $A, B$ is a necessary but not sufficient condition for confounding to take place. If it does take place, the covariates which are different are called confounders. The following conditions are necessary for a covariate to be considered a confounder:
1. The covariate causally affects the outcome $\mu$ within treatment groups.
2. The covariate is distributed differently across populations.

> *Some authors (e.g., Miettinen and Cook, 1981; Robins and Morgenstern, 1987) define a confounder more broadly, as any variable for which adjustment is helpful in reducing bias in effect estimation; variables that are confounders by virtue of their effects on the outcome parameter are then called causal confounders. Such broad definitions of confounders stem from recognition that confounding may be dealt with by stratification on variables that are not themselves causes of the outcome.* - Does this refer to my case, where the group variable does not cause the instance variable?