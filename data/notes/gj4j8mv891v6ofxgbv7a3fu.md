[S4] stands for "Efficiently Modeling Long Sequences with Structured State Spaces," an acronym coined in its publication of the same name by [Gu et al., 2021.][s4] This paper uses a continuous-time parametrization to model long-range dependencies in terms of multiple independent linear state space models in 1D sequences: But more importantly, the authors derive a practical optimization framework for such models that enables trivially data-parallel training and causal, autoregressive inference in $O(1)$ space by discretizing this continuous-time parametrization on-the-fly.

Causal convolutional kernels the same width as the input signal *at arbitrary timescales* are useful for fitting the model to signals causally during optimization, but alternatively, the underlying parameterization can be instead discretized as parameters for a *polynomial recurrence model* that explicitly stores the underlying "state" of the system between "transitions" (e.g., HiPPO kernels) between applications of the underlying discrete update step, or "state transitions—" allowing reconstruction of past context not only theoretically but *empirically.* This allows the model not only to scale log-linearly in the parameter count necessary to model the sequence length that it is expected to encounter. Deep SSMs provide a very promising alternative to transformer architectures, particularly for irregularly-sampled signals or extremely long contexts.

![S4](/assets/images/s4.png)

Offshoots include [S4D]. Gu et al. found that "restricting the [state transition matrix] to be fully diagonal can still preserve the performance of the original model." Empirically, this works best when the continuous-time parametrization of S4 is left at the mercy of a discrete input signal which does not obey so many temporally-correlated signals as to be encapsulated with only one state space model: I.e., rather than the problem requiring reconstruction of continuous patterns, it merely requires reconstructing a specific subset of discrete signals. Slimming down the intermediate S4 module is thereby sometimes empirically observed to have better convergence properties and make better use of the same number of parameters on language tasks. [Mehta, et al., 2022][gss] found that a learnable parameter, $\Delta,$ could even be completely fixed (set to 1) in their experiments without impacting performance— although they did acknowledge that they trained on relatively shorter sequence lengths, and used vastly more compute. 


![S4D](/assets/images/s4d.png)


### Arbitrary temporal masking

For self-attention models, it's trivial to prevent models from erroneously learning relationships between or within arbitrary points in a temporal sequence by adding a large bias to their intermediate attention logits, directly modifying the pointwise mutual information available to the model during training.

![Shin, et al., 2020.](/assets/images/diag_mask.png)

Preventing attention _between_ samples that occur in the same position within a minibatch using a method like [SPFHP] (Kosec, et al., 2021) may be possible with S4 by concatenating convolutional kernels sampled for two different temporal signals. It isn't as obvious how to prevent the model from erroneously learning relationships between points _within_ a sequence for which only one temporal kernel of uniform width can be computed, however, which may entail a need to compute multiple kernels of limited contextual length in order to perform arbitrary masking between points within a sequence (obviously not ideal).

Although [[ref.nlp.lae]] was originally intended for attention models such as transformers and their derivatives— which enjoy great ease of implementation for this method because of their explicit representation of the pointwise mutual information between discrete points within a given sequence— In principle, it could work for arbitrary sequence models if there were some way to "block" arbitrary points within a given sequence from influencing one another on a forward pass in the same way. For something like S4, the solution does not immediately present itself, although the problem of preventing such models from erroneously finding relationships _between_ samples within a forward pass seems less challenging, as one may simply choose to concatenate two convolutional kernels the same width as the respective temporal signals. 

[s4]: https://arxiv.org/abs/2111.00396
[s4d]: https://arxiv.org/abs/2206.11893
[gss]: https://arxiv.org/abs/2206.13947
[spfhp]: https://arxiv.org/abs/2107.02027
