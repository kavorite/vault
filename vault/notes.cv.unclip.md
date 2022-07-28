---
id: s2dvzt8effhbjxgsflxlw75
title: UnCLIP
desc: ''
updated: 1659017941664
created: 1658923989156
---

[Dall⋅E][paper] performs image generation and editing conditioned on semantic natural language prompts embedded in the prior given by a multimodal [[notes.cl.clip]] encoder. Most of the publication just talks about jointly training a transformer textual encoder with an image encoder. As seems to be OpenAI's trademark, most of this discussion is making a lot of hay over very little actual novelty in its methods, and is mostly just impressive in its thorough enumeration of implementation details and sheer scale. 

The real meat of the publication lies in the review of a number of different approaches from literature for methods of image synthesis ([paper] Section 2, "Method"), which reconstruct images by conditioning on both explicit textual prompts and latent multimodal embeddings. This process is not trained jointly with CLIP. Instead, the "text-image codebook" is learned ahead of time. [Classifier-free guidance][clfree] is implemented by randomly dropping CLIP embeddings during UnCLIP's training regime.

The best confluence of sample diversity, visual fidelity, and aesthetic ratings by human viewers was found to use an ensemble of [DDIM] models which feed forward into one another with intermediate steps which upsample to a higher resolution (64×64, 256×256, 1024×1024), although it is unclear from the paper exactly how each stage is parametrized. This three-stage pipeline and the intermediate upsampling steps are collectively called UnCLIP. In this regime, each successive upsampled image is noised essentially by applying a transposed block filter, rather than by directly sampling from a Gaussian distribution. 

Denoising the image via inpainting while reproducing the same semantics as the original content becomes a nontrivial, denoising-autoencoding objective for which diffusion models were found to be best suited overall. Perhaps a decoder could perform better by allowing the upsampling factor to be conditioned on the input using [[notes.opt.film]] and dynamically learned?

[paper]: https://arxiv.org/pdf/2205.12674.pdf
[ddim]: https://arxiv.org/abs/2010.02502
[clfree]: https://openreview.net/pdf?id=qw8AKxfYbI