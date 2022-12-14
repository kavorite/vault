---
id: 0oj3xw4fhwwb7qifcve8g19
title: Loss Conditioning
desc: ''
updated: 1659021548107
created: 1658887803982
---
[Loss-conditional training][blog] is a method which conditions a neural network on a hyperparameter vector **ɑ** (where **ɑ** > **0** and Σɑ = 1). [[ref.opt.film]] is used to condition a neural network on desired tradeoffs between multiple objectives at test-time through input of an arbitrary ɑ, and has even been observed to recover performance and teach more about the underlying semantics of a task by distilling knowledge of two separate objectives into deeper neural networks simultaneously. Performance generally suffers with networks that are not as deep.

[blog]: https://ai.googleblog.com/2020/04/optimizing-multiple-loss-functions-with.html