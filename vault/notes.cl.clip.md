---
id: 63z6zjmnp5tg1pj2rwcfb2f
title: CLIP
desc: ''
updated: 1659021328897
created: 1658923754928
---
Contrastive Language-Image Pretraining, or [CLIP], is a method which trains a language encoder jointly with an image decoder in a collaborative regime, distilling domain knowledge into an image encoder by using the language encoder's representations of image captions as a supervisory signal in a training regime almost identical to a parallel version of [[notes.cl.supcon]]. Unlike SCL and many related contrastive methods, CLIP has the distinction of embedding both input encoder representations into the same latent space, making it useful in multimodal modeling and conditioning generative applications on more than one type of support, as in [Dall-E]'s unCLIP.

[clip]: https://openai.com/blog/clip/
[dall-e]: https://openai.com/blog/dall-e/