# Self-Supervised Learning with Data Augmentations Provably Isolates Content from Style

[Arxiv Paper.](https://arxiv.org/pdf/2106.04619.pdf)

**Why?** 
- Reviewers at NeurIPS 2022 said I should use an identification theory like this one.
- This is also an example of a recent work on content-style disentanglement.
- It treats the subject from a causal inference perspective, which is what I want to do as well.
- It provides a dataset that I may use for my project.

**Summary**

Why does it work to train representation learning networks to be invariant to hand-crafted modifications on the input images? The papers aim to make a theory about this. They show that training with pairs of augmentations provably separates the content and style components of the representation. Their identification theory applies to nontrivial causal relationships. They also introduce an image dataset with such complex causal relationships.

## Formulation

Generative model: $\mathbf{x} = \mathbf{f}(\mathbf{z}), ~ \mathbf{z} \sim p_{\mathbf{z}}$. The function $\mathbf{f}$ is assumed to be an invertible mapping. <mark>I want to see what happens when we don't make this assumption.</mark>

Assume a family of transformations $\mathcal{T}$ such that $\tilde{x} = t(x)$ where the transformation leaves the part $c$ of the representation unchanged and may change part $s$.

**Def.** A content partition $c = f^{-1} (x)_{1:n_c}$ is *block-identified* by a function $g:\mathcal{X} \to \mathcal{Z}$ iff the inferred content partition $\hat{c} = g(x)_{1:n_c}$ has all and only the information in $c$. In the deterministic case, it means that there is an invertible function $h:\mathcal{Z} \to \mathcal{Z}$ matching the two content partitions $c = h(\hat{c})$.

**Theorem.** A learned representation $g(x)_{1:n_c}$ block-identifies the true content partition $f^{-1}(x)_{1:n_c}$ if:
- j