---
layout: post
title: "Google's smallest public LLM model and Meta's neural codec"
date: 2025-09-18
---

Last month Google released a compact version for the Gemma 3 large language
model (LLM) family with just 270 million parameters
([Gemma 3 270M](https://developers.googleblog.com/en/introducing-gemma-3-270m/)).
I'm amazed at the efficiency and potential for applications such as on-device
use.

I tried it a few days after the launch and found the default model's generated
text to be underwhelming for my prompts.  This confirmed to me the above blog's
explanation that the model targets fine-tuning applications.   I found other
reports that also expressed similar thoughts such as
[this post](https://shekhargulati.com/2025/08/15/i-tested-gemma-3-270m-on-the-simplest-nlp-task/).
Recently I cleaned up my code and published it to this
[`gemma3_270m` GitHub repo](https://github.com/guynich/gemma3_270m)
and my impression has improved on the default model performance, such as this
example.
```console
Model:        google/gemma-3-270m-it
Device:       mps:0
Precision:    torch.bfloat16
================================================================================
Input prompt: What causes climate change?
Climate change is caused by human activities, primarily the burning of fossil fuels.
```

I haven't identified a fine-tuning task for Gemma 3 270M but look forward to
working on that!  Especially now that Google has released the
[EmbeddingGemma](https://developers.googleblog.com/en/introducing-embeddinggemma/)
model so that direct comparison can be made between fine-tuning and retrieval
augmented generation methods for a specific task targetted for local on-device
implementation.

Separately it's been good to catch-up on technology for audio sound.
"Neural codecs" are encoder–decoder models that convert audio into compact
numeric representations (e.g.: quantized latent tokens or continuous latents)
which can be ingested and produced by large language models (LLMs). By letting
an LLM predict sequences of these audio tokens, the model can generate or
reconstruct audible sound.  For example Meta (formerly FaceBook) described
such technology in this
[2022 paper](https://arxiv.org/pdf/2210.13438) and released their
["EnCodec" implementation on GitHub](https://github.com/facebookresearch/encodec)
followed by a HuggingFace transformers version in June 2023.  I tried it out
and published my approach in this
[`encodec` GitHub repo](https://github.com/guynich/encodec) and was impressed by the
compact representation and quality at just 6 kbps.

I'm looking forward to more hands-on work with audio, speech and LLMs!
