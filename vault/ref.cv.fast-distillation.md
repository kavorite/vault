---
id: d2ujohiat60fr3984ndteed
title: Fast Knowledge Distillation for CNNs
desc: ''
updated: 1659021362340
created: 1653182223624
---
Using methods published by [Shen, et al., 2021,][paper] it's possible to distill knowledge more sample-efficiently, echoing [[ref.cl.moco#Fast-MoCo]]. The elevator pitch is that you create a pseudo-annotated dataset from many augmentations of the same image, alongside the output of the teacher's head, effectively creating many samples per forward pass of the teacher network, and allowing for a bespoke form of [[ref.opt.data-echoing]]: Images can be loaded once, resampled, and shipped over for preprocessing _on the hardware accelerator itself,_ effectively providing a built-in echoing factor of however many augmented views are taken per image. Since I generally already apply sample-specific augmentations on the device during data echoing, the main performance gains to be expected are those from applying the teacher network to cropped spatial regions of the input (jigsaw assembly, again, similar to [[ref.cl]]).
1. Apply a set of deterministic, pseudo-random data augmentations **with a predetermined seed,** if using a stochastic algorithm (e.g., [RandAugment]). For most training regimes, this also should include a (deterministic) random crop. 
2. Apply the teacher model; store extracted features alongside the augmentation hyperparameters (bounding boxes for cropping, transformations applied). In JAX, and other augmentation implementations with stateless PRNG, this could be as simple as making a note of the transformation [seed][jax-rng]. Persist the results to disk. 
3. Train the student model to emulate the output of the teacher. Can be done with standard KL divergence objectives or MSE for [logit cloning][cloning] if you're feeling *exotic.*

[jax-rng]: https://jax.readthedocs.io/en/latest/jax.random.html
[paper]: https://arxiv.org/abs/2112.01528
[randaugment]: https://github.com/4rtemi5/imax
[cloning]: https://arxiv.org/abs/2105.08919