---
id: iu6ldvp95326hayrcvy9lg0
title: Knowledge Distillation
desc: ''
updated: 1658950661986
created: 1653185716656
---
A method first appearing in a [paper of the same name][abstract] (Hinton et al., 2015), in which a large "teacher" model's predictions are used as pseudo-annotations for a more compact "student." Emphasis mine. The most common variant uses standard KL Divergence, but some research shows empirically that [logit cloning][cloning] using mean squared error (Kim, et al., 2021) may have better convergence properties. Emphasis mine.

> A very simple way to improve the performance of almost any machine learning algorithm is to train many different models on the same data and then to average their predictions. Unfortunately, making predictions using a whole ensemble of models is cumbersome and may be too computationally expensive to allow deployment to a large number of users, especially if the individual models are large neural nets. Caruana and his collaborators have shown that it is possible to **compress the knowledge in an ensemble into a single model** which is much easier to deploy and we develop this approach further using a different compression technique. We achieve some surprising results on MNIST and we show that we can significantly improve the acoustic model of a heavily used commercial system by distilling the knowledge in an ensemble of models into a single model. We also introduce a new type of ensemble composed of one or more full models and many specialist models which learn to distinguish fine-grained classes that the full models confuse. Unlike a mixture of experts, these specialist models can be trained rapidly and in parallel.

[abstract]: https://arxiv.org/abs/1503.02531
[cloning]: https://arxiv.org/abs/2105.08919