---
id: 1rm9i6wwcy7k2rkioy52rs3
title: Language Autoencoding
desc: ''
updated: 1658949026452
created: 1658941369199
---

**L**anguage **A**uto**E**ncoding, or LAE, is a transformer objective proposed by [Shin, et al., 2020][paper] for training self-attention mechanisms for bidirectional NLU by explicitly masking out dot-product self-attention matrices with large negative bias on the diagonal, essentially "disabling" the model's internal representation that tokens "attend" to themselves and requiring each token to be predicted from surrounding context. 

![Language Autoencoding, from Shin, et al.](/assets/images/lae.png)

Shin, et al. acknowledge the relatedness of their method to masked language modeling, or MLM, objectives such as the one used to fit [BERT] (Devlin et al., 2018), drawing the analogical relationship of autoencoders to denoising autoencoders. I suspect LAE may be a more sample-efficient and smoother objective than BERT, while not requiring the same computational overhead and mind-bending technical considerations as [XLNet], as it requires learning bidirectional representations between all tokens and introduces no incongruities between train- and test-time as BERT does with its `[MASK]` token.

Self-attention masks could also potentially be used for regularization along alternative methods that explicitly perturb input sequences such as [whole-word masking][masking] by being more selective about which positions are "masked" on the diagonal.

![Diagonal Masking, from Shin, et al.](/assets/images/diag_mask.png)

[paper]: https://arxiv.org/abs/2004.08097
[bert]: https://arxiv.org/abs/1810.04805
[masking]: https://arxiv.org/abs/1906.08101
[xlnet]: https://arxiv.org/abs/1906.08237