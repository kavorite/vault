---
id: 9cismp3jsqbqx1pyso6xdc4
title: Supervised Contrastive Learning
desc: ''
updated: 1659056602441
created: 1653188946537
---

[Khosla, et al., 2021][paper] ([blog]) verified that supervised instance discrimination is more sample-efficient than direct supervision and leads to more distinct class embeddings, even when a set of training labels is provided for input samples. The publication attributes this property to the high number of negative instance samples available for providing supervisory signal on _one another_ within a minibatch.

According to the developers of the [official implementation][github], at small minibatch sizes, a [[momentum encoder|ref.cl.moco]] and dictionary are necessary to attain competitive performance. However, it should be possible to offset this technical overhead and hyperparameter sensitivity in a multi-device training regime by performing a rendezvous to synchronize replicated latent representations across minibatches with functionality such as `jax.lax.all_gather`, or by adding more positive examples with strong data augmentation, akin to a supervised form of [[Fast-MoCo|ref.cl.moco#Fast-MoCo]]. 

It is unclear how the added positive examples would affect stability or performance— particularly with noisy labels or multiple labels assigned to training instances. To help correct for this, and because the supervisory signal may come from an underlying symbolic hierarchy with this method, it may be worth exploring projection of this method's latent embedding space onto a [[Poincaré ball|ref.opt.hyperbolics]].

![Supervised Contrastive Learning](/assets/images/supcon.png)

[blog]: https://ai.googleblog.com/2021/06/extending-contrastive-learning-to.html
[paper]: https://paperswithcode.com/paper/supervised-contrastive-learning
[github]: https://github.com/HobbitLong/SupContrast