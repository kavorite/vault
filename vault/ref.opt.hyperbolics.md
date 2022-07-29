---
id: ikhbh5ldwpxjjb3ev2aacu0
title: Hyperbolic Geometry
desc: ''
updated: 1659019753675
created: 1658836812312
---
Hyperbolic geometry is highly useful for capturing semantic relationships between items. Particularly for domains with latent hierarchies: This can include word embeddings, and indeed, all other manner of graph embeddings. The ubiquity of applications was somewhat surprising to be considering the relative rarity of applied examples.

The main limitation of projecting latent embeddings onto the Riemannian manifold is the need for specialized gradient descent methods such as [RSGD] ([tutorial]), which I suspect limits this method's accessibility by making it a little less "batteries-included" and sometimes incompatible with alternatives. Embedding latent representations with Hyperbolic metrics on a Poincaré ball can either be viewed as a blessing or a curse in practice, and its tradeoffs with Euclidean spaces are not always clear. But it's my opinion that most often, with data that fit exponential frequency distributions or adhere to explicit hierarchies as observed by [Nickel, et al., 2017][word-embeddings], the additional representational capacity when working on a fixed compute budget and within a fixed dimensionality is well worth the cost.

In Euclidean geometry, because of the expectation that points are normally distributed, they must be clustered extremely tightly in order to form distinct groups ([De Sa et al., 2018][tradeoffs]). This is rather unfortunate for methods such as [[ref.cl.supcon]], which rely explicitly on a small selection of samples having strong positive relationships, and everything else tending to be embedded very far away because of the ease with which clusters emerge on the Poincaré unit sphere as compared with the Euclidean unit sphere. [Some research][image-embeddings] suggests that this is not always practical. A small distance between hyperbolic embeddings on a unit Poincaré sphere captures not one, but two semantic properties: 
1. "betweenness" of an item with in a hierarchy, and
2. the "subtree" to which the item belongs.

Following is a graphic depicting the learning of Euclidean word embeddings.

![Euclidean word embeddings](/assets/images/euclidean.webp)

Notice how deviating from the origin quickly forces subspaces to the edges of the unit sphere. This pattern requires far fewer dimensions to capture using hyperbolic geometry to distance neighborhoods from one another on a hyperbolic sphere, because it allows distances between neighborhoods to be defined by their centrality _with respect to the origin._ Contrast below.

![Hyperbolic word embeddings](/assets/images/hyperbolic.webp)

This means hyperbolic geometry allows for more efficient embedding of latent hierarchies, which is reflective of many long-tailed frequency distributions. Natural language corpora, for example, contain latent hierarchies, because "chinchilla" is a type of "mammal." Controlling for this property is important in a variety of information retrieval applications, most notably [bag-of-words document vectorization][tfidf].

![English word frequencies](/assets/images/word_frequency.png)

Certain publications have gotten around this by using bespoke loss functions to explicitly model the hierarchy of labels (e.g., for [ImageNet pretraining][pretraining]), but that takes a lot of effort: and it only encapsulates the hierarchies that are imposed by engineers, which doesn't allow models to efficiently _learn_ latent hierarchies from supervisory signals that may contain many latent hierarchical relationships, yet explicitly offer explicit insight into very few by way of supervisory signals. Hyperbolic embeddings are not just a way to regularize a somewhat noisy solution space, but also a promising approach to allowing our optimizers more degrees of freedom in designing good solutions, taking the effort of imposing hierarchical domain models for symbolic data through explicit use of "SynSets" out of our own hands.

[rsgd]: https://arxiv.org/abs/1806.03417
[tutorial]: https://lars76.github.io/2020/07/23/rsgd-in-pytorch.html
[tradeoffs]: https://arxiv.org/abs/1804.03329
[pretraining]: https://arxiv.org/abs/2104.10972
[word-embeddings]: https://arxiv.org/abs/1705.08039
[image-embeddings]: https://arxiv.org/abs/1904.02239v2
[tfidf]: https://tfidf.com
