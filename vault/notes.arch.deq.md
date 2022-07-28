---
id: vl3h77sg0urrzngvpa94cp0
title: Deep Equilibrium Models
desc: ''
updated: 1659021571317
created: 1658837430978
---
**D**eep **Eq**uilibrium Models, or DEQs, were introduced in [Bai et al., 2019][deq]. They exploit the observation that conventional, or "explicit," deep neural networks in practice generally coerce their intermediate state to a fixed point of "equilibrium." Framing residual blocks as $f(z_i, x_i) = f(z_{i}) + x_{i-1}$,  the paper casts neural networks as fixed-iteration solvers that iterate $z_0 \ldots z_n$ toward some $z^\star$ at their output layer, and observes that to that end, the intermediate layers of neural networks often learn redundant and repeated transformations, which undermines the "mixture of experts" theory commonly understood to justify the performance of DNNs. 

Due to the proliferation of intermediate normalization and residual connections in state of the art overparametrized models, reapplying the same operations to different inputs over and over again is often stable, with predictable, bounded outputs. This is what makes modern topologies converge despite their depth. This allows the equilibrium point to be solved for explicitly with multiple forward passes of the same layer and associated weights, while backpropagation is done using implicit differentiation. Hence, the distinction between "explicit" and "implicit" neural networks.

In practice, while it is perhaps somewhat surprising that a single residual layer being reapplied multiple times can represent a neural network of arbitrary depth, a fixed-scale residual block can reduces memory required for forward and backward passes to $O(1)$, and often converges to just as good a solution, although [[some adjustments|notes.arch.deq.extensions]] are necessary to keep training stable and efficient, such as explicit regularization of the Jacobian.



[deq]: https://arxiv.org/abs/1909.01377
[tutorial]: http://implicit-layers-tutorial.org/deep_equilibrium_models/
