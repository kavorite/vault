---
id: uihquvh4fwgniynh3aly42g
title: MoCo
desc: ''
updated: 1659031936204
created: 1653189552070
---
Introduced by He, et al., 2019, [MoCo], or **Mo**mentum **Co**ntrast, uses a set of "slow" and "fast" parameters. A "slow" momentum encoder, with a small update rate of ρ ≤ 0.01, is interpolated toward the latest parameter vector at each descent step, and to perform self-supervised instance discrimination, its embeddings are used as supervisory signals. Like [[ref.cl.supcon]], it required large training batches, which its authors would attempt to rectify in MoCov2.

## Derivatives
### [MoCov2]
Introduced by (Chen et al., 2020), the momentum encoder is used to enqueue old embeddings to gradually build a "dictionary" of negative samples, pushing future representations away from the past. An MLP projection head and stronger data augmentations were used. 

![MoCov2](/assets/images/mocov2.png) 

### [SimMoCo and SimCo][simco]
Zhang, et al., 2022 eschew MoCov2's addition of a "negative dictionary" in favor of a "dual-temperature" approach. Their publication also contains a helpful rundown of the wider self-supervised contrastive literature (Section 7, "A Unified Perspective on SSL and Beyond").

### [Fast-MoCo]
This method, published by Ci et al., 2022, bears some resemblance to [[ref.cv.fast-distillation]] and FAIR's [DINO] ([blog][dino-blog]; Caron et al., 2021) with its self-supervised "collage assembly" objective, applying InfoNCE to multiple augmented views of a set of objects.

--- 
[moco]: https://arxiv.org/abs/1911.05722
[mocov2]: https://arxiv.org/abs/2003.04297
[simco]: https://arxiv.org/abs/2203.17248
[fast-moco]: https://arxiv.org/abs/2207.08220
[dino]: https://arxiv.org/abs/2104.14294
[dino-blog]: https://ai.facebook.com/blog/dino-paws-computer-vision-with-self-supervised-transformers-and-10x-more-efficient-training/