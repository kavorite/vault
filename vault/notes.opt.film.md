---
id: zy4oqk1z59whxqbjtmwbdm4
title: Feature-wise Linear Modulation
desc: ''
updated: 1659021537619
created: 1658887070728
---
[FiLM], or **F**eature-wise **L**inear **M**odulation, is a method of injecting intermediate support information for a task into a visual feature extraction pipeline which learns multiple conditioning steps at intermediate layers that teach neural networks to view their inputs through a user-specified support 'lens.' It has proven useful, for example, in training DNNs to fit to [[multiple objective functions simultaneously|notes.opt.loss-conditioning]], such that the tradeoff between objectives can be adjusted at inference-time.

[film]: https://arxiv.org/abs/1709.0771