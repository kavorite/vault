---
id: vl3h77sg0urrzngvpa94cp0
title: Deep Equilibrium Models
desc: ''
updated: 1659409731780
created: 1658837430978
---
**D**eep **Eq**uilibrium Models, or [DEQs][tutorial], were introduced in [Bai et al., 2019][paper]. They exploit the observation that conventional, or "explicit," deep neural networks in practice generally coerce their intermediate state to a fixed point of "equilibrium." The publication builds on the conception of neural networks proposed by [He, et al., 2015][resnets] as a series of residual functions $f(\textbf{z}_i, \textbf{x}_i) = f(\textbf{z}_{i}) + \textbf{x}_{i-1}$. The authors characterize such residual networks as fixed-iteration solvers that push $\textbf{z}_0 \ldots \textbf{z}_n$ toward some 'point of equilibrium' $\textbf{z}^\star$ at their output layer. The DEQ authors motivate this generalization by the fact that intermediate layers of neural networks often learn redundant and repeated transformations ([Parnami, et al., 2021][redundancy]), which is somewhat surprising, undermining the "mixture of experts" theory commonly understood to justify the performance of DNNs.

Residual architectures proliferate throughout across a wide variety of tasks in literature. Their ubiquity cannot be overstated: After the watershed moment the first ResNets brought about in image recognition they were adapted to many other applications. Currently, the overall "residual" structure of backbones whose layers propagate intermediate information through a form of 'skip connection' includes models used in [natural language processing][berts], [recommender systems][cross], [audio classification][audio], and many more: All can be said to trace a common lineage back to the tradition of the first convolutional ResNets. 

Due to the proliferation of intermediate normalization and residuals in state of the art overparametrized models, reapplying the same "residual block" of a given neural network to different inputs over and over again is often stable, with predictable, bounded outputs. This is what makes modern topologies converge despite their depth. In the tradition of weight sharing and "reversible" methods such as those proposed by [Sander, et al., 2021][rhonets] and [Reid, et al., 2021][sharing], and echoing [early exit][exits] literature, Bai, et al. contend that $\textbf{z}^*$ can be solved for explicitly with multiple forward passes of the same layer and associated weights, while backpropagation is done using implicit differentiation... for *any type of neural network.* Hence, the distinction between "explicit" and "implicit" methods. 

In practice, while it is perhaps somewhat surprising that a single residual layer being reapplied multiple times can represent a neural network of arbitrary depth, the use of a fixed-scale residual block recovers the $O(1)$ memory footprint and performance of previous works based on "reversible" explicit differentiation, often converging to just as good a solution— although [[some adjustments|ref.arch.deq.extensions]] are necessary to keep training stable and efficient, such as explicit regularization of the Jacobian. 



[audio]: https://arxiv.org/abs/2106.01621
[cross]: https://arxiv.org/abs/1708.05123
[paper]: https://arxiv.org/abs/1909.01377
[berts]: https://jalammar.github.io/illustrated-bert/
[exits]: https://arxiv.org/abs/2004.12993
[resnets]: https://arxiv.org/abs/1512.03385
[rhonets]: https://arxiv.org/abs/2102.07870
[sharing]: https://arxiv.org/abs/2101.00234
[redundancy]: https://arxiv.org/abs/2110.15225
[tutorial]: http://implicit-layers-tutorial.org/deep_equilibrium_models/
