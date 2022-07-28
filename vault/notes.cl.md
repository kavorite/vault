---
id: jc56h8njgqawadlroex4ju1
title: Cl
desc: ''
updated: 1659015136447
created: 1658948027342
---

This section is generally dedicated to discussing methods for learning _by contrast._ For example, in standard supervised classification, we backpropagate against a loss function that evaluates the divergence between a discrete probability distribution: one matrix of **predictions** $P ∈ ℝ^{b × n}$, and one matrix of **targets** $T ∈ \{0, 1\}^{b × n}$. 

It's often found that this can be less sample-efficient: after all, this supervisory signal embeds no explicit information about what in a minibatch is related to whatever else, it only forces exact and explicit replication of human judgments. Each sample only informs the model's predictions of _that sample_ (conditional independence). Surprisingly, this is error metric is generally noisier and harder to fit than the alternative metrics resulting from _using the same core idea of divergence between probability distributions,_ but first, applying a few simple transformations, such that the distributions reflect whether two items are "similar" or not, rather than annotations of where they lie in some arbitrary ${0,\ 1}^n$ label space.

First it can be more numerically stable to project $P$ to lie on the unit hypersphere by normalizing the feature-wise magnitudes of its sample embeddings:
$$
P_{i,j} ← \frac{P_{i,j}}{||P_{:,j}||_2}
$$

Such that $PP^T$ will contain the pairwise cosine similarities of all the entries in any given batch of label logits $P_{b × n}$— or more commonly, $P_{b×d}$, where $d$ is some arbitrary, latent dimensionality. Then, instead of directly classifying $P$ and $T$, one _instead_ evaluates $PP^T$ for its fit to $TT^T$, using the objective of choice (usually some variant of softmax cross-entropy).

The result is a feature extractor whose latent representations project "like" and "unlike" items into spatially distinct regions on the unit hypersphere, or even potentially some non-Euclidean space, like [[the Riemannian manifold|opt.hyperbolics]]. This can be used to perform few-shot classification by examining distances of new instances to a set of a few "exemplars" in embedding space, or, as in [[notes.cl.supcon]], simply fed forward into a linear classifier to use the stronger supervisory signal offered by pairwise instance discrimination for more robust generalization performance.

There are also variants, such as [[notes.cl.moco]], which simply treat augmentations of the same sample as 'positive' during instance discrimination rather than relying on explicit support from human annotations (an objective formulation called InfoNCE). 