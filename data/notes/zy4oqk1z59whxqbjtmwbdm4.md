[FiLM], or **F**eature-wise **L**inear **M**odulation (Perez, et al., 2017) is a method of injecting intermediate support information for a task into a visual feature extraction pipeline. This is accomplished by introducing a generator network which "modulates" feature-wise normalization parameters according to some continuous function conditioned on arbitrary data. Continuous 'modulations' of input samples were used in the original publication to condition neural networks on task specific information, sideloading semantically relevant 'queries.'

## Applications
[FiLM] has proven useful in training DNNs to fit to [[multiple objective functions simultaneously|ref.opt.loss-conditioning]], such that the tradeoff between objectives can be adjusted at inference-time, and in [deep ensembling][filmens] (Turkoglu et al., 2022), where multiple sets of normalization parameters can be learned in order to emulate multiple instantiations of a given model while sharing the rest of the parameter set. A forward pass is required for each set of learned "feature modulations," but the additional performance gains come at a predetermined, fixed-parameter cost. 


[film]: https://arxiv.org/abs/1709.0771
[filmens]: https://arxiv.org/abs/2206.00050