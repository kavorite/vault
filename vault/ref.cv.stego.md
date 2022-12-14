---
id: hqv5s3hlhjqatutciw4x4nm
title: STEGO
desc: ''
updated: 1659833555302
created: 1653185965558
---
Introduced in [Hamilton, et al., 2022][paper] ([blog]), **S**elf-supervised **T**ransformer with **E**nergy-based **G**raph **O**ptimization, or STEGO, can induce semantic segmentations by fitting a new head to a pretrained image recognizer, allowing it to be trained with tiny datasets on commodity hardware after a more costly classifier pretraining step. 

The reference implementation may be somewhat dependent on a fixed sampling resolution within the image encoder, which could potentially limit the method to use in tandem with Vision Transformers or fixed-width [[ref.arch.ckconv]] á la FlexConv (Romero, et al., 2021). However, upsampling the intermediate feature maps of a vanilla CNN to match the spatial resolution of the input might yield similar (although somewhat pixellated) results. I have not conducted my own experiments, I just figure there's probably _some_ reason they put the T in STEGO other than for the sake of the sexy backronym... I hope. 

> Unsupervised semantic segmentation aims to **discover and localize semantically meaningful categories within image corpora without any form of annotation.** To solve this task, algorithms must produce features for every pixel that are both semantically meaningful and compact enough to form distinct clusters. Unlike previous works which achieve this with a single end-to-end framework, we propose to separate feature learning from cluster compactification. Empirically, we show that current unsupervised feature learning frameworks already generate dense features whose correlations are semantically consistent. This observation motivates us to design STEGO (&(**S**elf-supervised **T**ransformer with **E**nergy-based **G**raph **O**ptimization), a novel framework that distills unsupervised features into high-quality discrete semantic labels. At the core of STEGO is a novel contrastive loss function that encourages features to form compact clusters while preserving their relationships across the corpora. STEGO yields a significant improvement over the prior state of the art, on both the CocoStuff and Cityscapes semantic segmentation challenges.

[blog]: https://wpthemeblog.com/mit-team-introduces-stego-an-algorithm-that-can-jointly-detect-and-segment-things-down-to-the-last-pixel-without-any-human/
[paper]: https://arxiv.org/abs/2203.08414