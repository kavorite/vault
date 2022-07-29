---
id: txmy1anxf7bhr607yyk7te7
title: DEQ Extensions
desc: ''
updated: 1659114708281
created: 1658945653478
---

## [Jacobian Regularization][jacreg]
DEQs turned out not to work especially well in practice, learning hard-to-solve Jacobian matrices, which caused training to lose stability and become less computationally tractable over time. Bai et al., the same research group which invented DEQs, later presented methods that allow this behavior to be explicitly regularized, bringing their computational costs to par with those of explicit networks.

## [IMEX]
Introduced by Pal, et al., 2022, IMEX combines DEQs with an explicit correction layer which conditions them on their inputs and predicts initial hidden states, not unlike [[ref.opt.film]], stabilizing and expediting training.

## [MDEQ]

I'm somewhat unimpressed with MDEQ. I don't think that downsampling to multiple resolutions at the input with weight-tying is the best way to exploit relationships between different feature scales. Resampling the input just so that it can be passed through the same DEQ cell layer multiple times in parallel results in loss of some simplicity compared to baseline explicit methods such as vanilla ResNets, which can just use intermediate downsampling during forward propagation. Romero, et al., 2021 observe a poor generalization performance between multiple feature scales in discrete convolutions. One could replace [MDEQ]'s approach of backpropagating through multiple feature resolutions simultaneously with something more akin to their [[FlexConv|ref.arch.ckconv]].

#### [[SAM|ref.opt.sam]] 
Other forms of explicit regularization might also be of use in combination with explicit regularization of the Jacobian: I'm not sure SAM has ever been applied in tandem with implicit differentiation, but I'm also not sure why it wouldn't work in principle. As noted by Bai, et al., more conventional regularization techniques such as weight standardization and feature- and batch-wise normalization are critical for convergence of "vanilla" DEQs in practice, pointing to a relationship between the explicit "differentiability" of deep neural networks when taken as fixed-iteration equilibrium solvers, and the ease of explicitly solving for points of equilibrium in DEQs. I would trade compute off for reliability, hyperparameter-stability, and sample efficiency any day of the week, implicit backpropagation or not. Perhaps I should more deeply explore whether this is possible. 

[mdeq]: https://arxiv.org/abs/2006.08656
[jacreg]: http://implicit-layers-tutorial.org/deep_equilibrium_models/
[imex]: https://arxiv.org/abs/2201.12240