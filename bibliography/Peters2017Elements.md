# Elements of Causal Inference

## 5.2 Covariate Shift

**Principle 2.1** If the joint distribution $P_{\mathrm{cause, effect}}$ changes across domains, then $P_{\mathrm{cause}}$ and $P_{\mathrm{effect} | \mathrm{cause}}$ change independently.

If $X$ is the cause and $Y$ is the effect, then regardless of changes in the distribution of $X'$, $P_{Y | X}$ is still the best guess for $P_{Y' | X'}$. This is a well-studied assumption in Machine Learning that is only appropriate in the causal scenario.

If, however, $X$ is the effect and $Y$ is the cause, changes in $P_X \to P_{X'}$ become informative about $P_{Y' | X'}$. This is the anticausal scenario.

> *Conceiving of general methods exploiting the fact that $P_{\mathrm{effect}}$ and $P_{\mathrm{cause} | \mathrm{effect}}$ change in a dependent way is a hard problem.* - This is exactly what my instance encoder is doing.