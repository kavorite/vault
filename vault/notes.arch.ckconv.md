---
id: kxklakzrojw3q2r808mzh65
title: Continuous Kernel Convolution
desc: ''
updated: 1659020720817
created: 1658835909947
---
Continuous-kernel convolutions are just that: Convolutions with a continuous kernel. The kernel is determined by a **generator network** with a fixed parameter cost, by composing a learned linear operator with a predetermined gaussian mask, such as a blur filter, or an (optionally steerable) Gabor filter as in [Romero, et al., 2021's][flexconv] **M**ultiplicative **A**nisotropic **G**abor **N**etworks, or MAGNets.

![FlexConv parametrization](/assets/images/flexconv.png)

In order to sample a kernel, a small, feed-forward subnetwork is used to map relative spatial coordinates sampled at some discrete rate— e.g., a grid on [-1, 1]— to intensities within the desired output space. The output of the MLP can be stabilized with methods such as LayerNorm, weight standardization etc., but the important bit is that the MLP learns a continuous function that maps points in coordinate space to some learned intensity for the output kernel at the given point, rather than fixing the kernel's size and depth and learning the values of each constituent point within the kernel's volumetric mapping individually. 


## Computational Caveats
Romero, et al. observed based on the states of converged FlexConvs that they tended to learn larger receptive fields as one descends deeper into their architecture during training, at least on natural images. This presented a problem: It slowed things down. The computational overhead of convolutions scales cubically with kernel size, and the only hard upper bound is the input sampling resolution.

![Progressively Larger Kernel Sizes](/assets/images/progressive-kernel-sizes.png)

This cost could of course be offset with downsampling, but [CCNN] offers evidence that depthwise-separable versions of [FlexConv] kernels, or FlexSepConv, can be combined with global kernel sizes or depthwise-separable convolutions in order to offset the computational cost of large kernels, making it quadratic instead. The size of the receptive field produced by kernel generator networks like MAGNets could additionally be conditioned on its inputs with intermediate componentry akin to [[notes.opt.film]], or explicitly regularized with an additional loss term, leading me to ask what the result would be if these architectures were trained with [[notes.opt.loss-conditioning]].


[flexconv]: https://arxiv.org/abs/2110.08059
[ccnn]: https://arxiv.org/abs/2206.03398