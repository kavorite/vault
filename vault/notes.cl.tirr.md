---
id: hwm8yedokqpoldsx5rsjghh
title: TIRR
desc: ''
updated: 1659019558101
created: 1658923518236
---
TIRR, or "Temporal Image-Based Recommender," is a mutual recommender system published by [Neve, et al., 2021][paper]. It is built from the ground up for conditioning on individual preferences to recommend _people_ to _one another_ by conditioning on associated samples of their content, making it instantly useful for content aggregation and social media applications.

There are many technical extensions and improvements that can be made. For example, it only uses photographs, not natural-language descriptions. The kernel tricks employed by LSTMs and GRUs in order to give them "long term" memory by emulating tracing patterns observed in mammalian cognition actually forget rather quickly, making integration of a method such as [[notes.arch.s4]]'s HiPPO potentially somewhat useful, both for condition predictions on longer historical contexts and use convolutions for training in parallel. 

This ordinarily "catastrophic" forgetting could, however, be seen as favorable for a temporal model which must rapidly learn to condition new predictions on user preference within one session of use and adapt to changing preferences in real-time: causal autoregression in fixed memory at test-time may be the most important pragmatic consideration.

![TIRR's architecture](/assets/images/tirr.png)
[paper]: https://arxiv.org/abs/2108.11714