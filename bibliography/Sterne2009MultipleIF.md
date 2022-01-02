# Multiple imputation for missing data in epidemiological and clinical research: potential and pitfalls

[Semantic Scholar](https://api.semanticscholar.org/CorpusID:31568154)

## Types of data missingness

Data can be missing in multiple ways depending on the probabilistic relationship between the missingness and the observed and unobserved variables.
1. **Missing Completely at Random:** The missingness is independent of any variable of interest. **e.g.** Blood pressure readings may be missing because the equipment is broken.
2. **Missing at Random:** The missingness is dependent on some observed variables but independent of the unobserved variables. **e.g.** Missing measurements might be lower than measured just because young people take fewer measurements.
3. **Missing Not at Random:** The missingness also depends on unseen variables. **e.g.** People with low blood pressure might take fewer measurements because they are healthier.

## Statistical methods to deal with missing data

Using only complete data when the data is missing not completely at random leads to biased results. Sometimes analysis of complete data does not lead to bias.
1. When there is missingness only in the outcome variable (and only one outcome value per individual), the observed variables can be used as covariates and MAR does not lead to bias.
2. Missing data in covariates also does not necessarily cause bias if the missingness is independent of the outcome.

There are multiple ways to learn from incomplete data.

## Multiple imputation