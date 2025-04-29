#  Multi-Level Variational Autoencoder: Learning Disentangled Representations from Grouped Observations
**Link:** https://api.semanticscholar.org/CorpusID:1209557
**Author:** Bouchacourt
**Subject:** [[group_instance_disentanglement]]

## Accumulating evidence for group variable
- We're trying to break this down $$q(\textbf{u}^n|\underline{\textbf{x}}^n) = \frac{q(\textbf{u}^n)}{q(\underline{\textbf{x}}^n)} q(\underline{\textbf{x}}^n|\textbf{u}^n) = \frac{q(\textbf{u}^n)}{q(\underline{\textbf{x}}^n)} \prod_{k=1}^{K_n} q(\textbf{x}_i^n|\textbf{u}^n)$$
	- One thing we could do is invert it again so that we sample a group variable from each observation $$q(\textbf{u}^n |\underline{\textbf{x}}^n) = \frac{q(\textbf{u}^n)}{q(\underline{\textbf{x}}^n)} \prod_{k=1}^{K_n} \frac{q(\textbf{x}_k^n)}{q(\textbf{u}^n)} q(\textbf{u}^n | \textbf{x}_k^n)$$ $$=  \underbrace{\frac{\prod_{k=1}^{K_n} q(\textbf{x}_k^n)}{q(\underline{\textbf{x}}^n)}}_{\text{constant wrt u}} q(\textbf{u}^n)^{1 - K_n} \prod_{k=1}^{K_n} q(\textbf{u}^n | \textbf{x}_k^n)$$
- They're saying that $$q(\textbf{u}^n | \underline{\textbf{x}}^n) \propto \prod_{k=1}^{K_n} q(\textbf{u}^n | \textbf{x}_k^n)$$ **but I don't think this is true!**



