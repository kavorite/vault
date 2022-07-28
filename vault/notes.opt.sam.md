---
id: 3cublmnyywkz5grltuf1253
title: Sharpness Aware Minimization
desc: ''
updated: 1658983692345
created: 1653183250379
---
**S**harpness **A**ware **M**inimization, or SAM, is a regularization technique introduced by [Foret, et al., 2020][abstract] used to train models which have the same generalization ability under datasets that are up to an order of magnitude smaller. The algorithm is so simple I have [implemented it myself,][implementation] and I can describe it here:
1. Requirements:
    1. $V \coloneqq$ the set of model parameters $\textbf{w}_0, \textbf{w}_1\ldots \textbf{w}_n$
    2. $\textbf{v} \coloneqq$ global parameter vector (flatten/concat $\textbf{w}_i \in V$)
    3. $\rho \coloneqq$ A hyperparameter. Authors usually set to 0.05.
2. Until converged:
    1. Take a small, $\rho$-sized ascent step:
        $$
        \textbf{w}_i
        \leftarrow
        \textbf{w}_i 
        + \rho
        \frac
            {\nabla_{L}\textbf{w}_i}
            {||\textbf{v}||_2}\
        \forall\ \textbf{w}_i \in V
        $$
    2. Take an actual *descent* step using an "inner" optimizer, like SGD. This is typically more involved, but also better-studied (see review by [Ruder, et al., 2016][optimizers]).

To say nothing of how a more stable training regime helps address the ongoing replicability crisis in deep learning, using SAM also means less training time. 

This means despite SAM's requirement of twice as much compute per forward-backward pass, in effect taking one step back for every step forward, the technique's uncanny ability to converge to a superior and more stable performance within half as many steps suggests that the method's sample efficiency offers some potential to help this method cut some costs despite itself, especially in terms of data procurement. [LookSAM] can help offset those compute costs if you're pulling your hair out over it.

![Left/Right: SGD/SA-SGD](/assets/images/sam.png)

Left/Right: Visualizations of loss landscape surrounding trained ResNet, contrasting SGD/SA-SGD, from Foret, et al. Wider, deeper minima result in better calibrated models with more generalizable decision boundaries.

## Derivatives and Extensions
### [LookSAM] 
Liu, et al., 2022 use a projective approximation to compute the ascent gradient every *k* steps instead of re-computing it every time a step is taken. Shameless self-plug, my [implementation] includes an interface to this functionality.

### [ASAM]
**A**daptive SAM, introduced by Kwon, et al., 2021, re-weights the ascent directions by a more complex formula for each parameter norm rather than using the global norm. My [implementation] also includes a variant of this.

### [δ-SAM][dsam]
SAM with dynamic reweighting by Zhou, et al., 2021— I'll be honest, I just stopped reading this one as soon as I saw it required doing three forward passes. 

[Abstract]: https://arxiv.org/abs/2010.01412
[ASAM]: https://arxiv.org/abs/2102.11600
[DSAM]: https://arxiv.org/abs/2112.08772
[LookSAM]: https://arxiv.org/abs/2203.02714

[implementation]: https://github.com/kavorite/sam
[optimizers]: https://arxiv.org/abs/1609.04747
