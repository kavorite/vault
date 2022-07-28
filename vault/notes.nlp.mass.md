---
id: epxo6h3psotasf3y7z98ect
title: MMASS
desc: ''
updated: 1658950183377
created: 1658949602554
---
[Siddhant, et al., 2022][paper], explore the applications of adding **M**ore MASS to methods originally introduced by [Song, et al., 2019][mass] (emphasis mine, they don't have a fun backronym). On multilingual, semi-supervised NMT, state of the art generalization was reported across arbitrary language pairs by applying self-supervised denoising-autoencoder objectives to high-resource language datasets. Their complaint about the "unscalability" of data procurement for low-resource languages seems to be openly taking aim at [M2M100], introduced by Fan, et al., 2020.

> Achieving universal translation between all human language pairs is the holy-grail of machine translation (MT) research. While recent progress in massively multilingual MT is one step closer to reaching this goal, it is becoming evident that extending a multilingual MT system simply by training on more parallel data is unscalable, since the availability of labeled data for low-resource and non-English-centric language pairs is forbiddingly limited. To this end, we present a pragmatic approach towards building a multilingual MT model that covers hundreds of languages, **using a mixture of supervised and self-supervised objectives, depending on the data availability for different language pairs.** We demonstrate that the synergy between these two training paradigms enables the model to produce high-quality translations in the **zero-resource setting,** even surpassing supervised translation quality for low- and mid-resource languages. We conduct a wide array of experiments to understand the effect of the degree of multilingual supervision, domain mismatches and amounts of parallel and monolingual data on the quality of our self-supervised multilingual models. To demonstrate the scalability of the approach, we train models with **over 200** languages and demonstrate high performance on zero-resource translation on several previously under-studied languages. We hope our findings will serve as a stepping stone towards enabling translation for the next thousand languages.

[paper]: https://arxiv.org/abs/2201.03110
[mass]: https://arxiv.org/abs/1905.02450
[m2m100]: https://arxiv.org/abs/2010.11125