---
id: txmy1anxf7bhr607yyk7te7
title: DEQ Extensions
desc: ''
updated: 1659577648992
created: 1658945653478
---

## [Jacobian Regularization][jacreg]
DEQs turned out not to work especially well in practice, learning hard-to-solve Jacobian matrices, which caused training to lose stability and become less computationally tractable over time. Bai et al., the same research group which invented DEQs, later presented methods that allow this behavior to be explicitly regularized, bringing their computational costs to par with those of explicit networks.

## [SkipDEQ][fastdeq]
Introduced by Pal, et al., 2022, [SkipDEQs][fastdeq] combine DEQs with an explicit correction layer which conditions them on their inputs and predicts initial hidden states, not unlike [[ref.opt.film]], stabilizing and expediting training. It is [implemented][fastdeq-impl] in Julia. Based on the difficulties that vanilla DEQs have with matching the computational efficiency of deep explicit models, all practical implementations of DEQs should probably look something like this.

## [MDEQ]

I'm somewhat unimpressed with MDEQ. I don't think that downsampling to multiple resolutions at the input with weight-tying is the best way to exploit relationships between different feature scales. Resampling the input just so that it can be passed through the same DEQ cell layer multiple times in parallel results in loss of some simplicity compared to baseline explicit methods such as vanilla ResNets, which can just use intermediate downsampling during forward propagation. 

MDEQ's construction is motivated by an observation of poor generalization performance between multiple feature scales in discrete convolutions in an environment where applications of convolutions are dominated by tasks where scale invariance is highly desirable, leading [He, et al., 2015][resnets] and many others to perform intermediate downsampling, introducing explicitly hierarchical patterns to how spatially correlated inputs are processed. Aggressive downsampling leads both to considerable improvements in both computational tractability and feature reuse: A success replicated many times over both in discriminative and generative image processing applications, including by UNets, proposed by [Ronneberger, et al., 2015][unets], NVAE, by [Vahdat and Kautz, 2020][nvae], and [[ref.cv.unclip]], by Ramesh, et al., 2022.

On that basis, one might replace [MDEQ]'s approach of backpropagating through multiple predefined feature resolutions simultaneously with something more akin to a [[FlexConv|ref.arch.ckconv]], instead, which takes the analogous approach of simply broadening the receptive field with increasing depth using continuous kernels that boast a fixed parameter cost, or even explicitly parametrize over the spatial downsampling factor at each step, while constraining resolution to lie above some fixed threshold, reducing the number of hyperparameters required for intermediate pooling while keeping most, if not all of the resulting representational capacity and computational dividends.

#### [[SAM|ref.opt.sam]] 
Other forms of explicit regularization might also be of use in combination with explicit regularization of the Jacobian: I'm not sure SAM has ever been applied in tandem with implicit differentiation, but I'm also not sure why it wouldn't work in principle. As noted by Bai, et al., more conventional regularization techniques such as weight standardization and feature- and batch-wise normalization are critical for convergence of "vanilla" DEQs in practice, pointing to a relationship between the explicit "differentiability" of deep neural networks when taken as fixed-iteration equilibrium solvers, and the ease of explicitly solving for points of equilibrium in DEQs. I would trade compute off for reliability, hyperparameter-stability, and sample efficiency any day of the week, implicit backpropagation or not. Perhaps I should more deeply explore whether this is possible. 

[mdeq]: https://arxiv.org/abs/2006.08656
[jacreg]: http://implicit-layers-tutorial.org/deep_equilibrium_models/
[fastdeq]: https://arxiv.org/abs/2201.12240
[fastdeq-impl]: https://github.com/SciML/DeepEquilibriumNetworks.jl
[resnets]: https://arxiv.org/abs/1512.03385
[unets]: https://arxiv.org/abs/1505.04597
[nvae]: https://arxiv.org/abs/2007.03898