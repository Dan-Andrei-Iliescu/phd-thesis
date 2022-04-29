# Data Analysis Using Multilevel Models

## Why?

A multilevel model is a regression model whose parameters are also regression models. They don't distinguish between fixed effects and random effects because all effects are random effects.

### 1.3 Motivations for multilevel modelling

1. Estimating treatment effects that vary by group. In classical statistics, this can be modelled with *interactions*. For example, a particular school policy might be more helpful to students in 8th grade rather than 2nd grade.
2. Efficient inference of parameters. *Complete pooling* ignores variation between groups and *no pooling* gives unacceptably variable inferences, especially in groups with few examples.
3. Prediction for a given group or a new group.
4. Accurately accounting for uncertainty. Variability might differ across groups.