---
layout: post
title: "Moonshine.ai adds streaming to their speech model"
date: 2026-02-11
---

A real **wow** moment for me.

I learnt last week from the team at Moonshine.ai about their newly released
**streaming** encoder "v2" implementation of the Moonshine automatic speech
recognition model.

Streaming enables efficient compute and low latency.  Through bounding the input
context to the transformer model encoder, streaming avoids repetitive/redundant
computation over earlier speech. It is an important requirement for efficient
on-device implementation such as in a smartphone (e.g.: for real **product**).

This new model matches the performance of models 4x the size while running 3x-8x
faster.  As ever it is revealing to use standardized comparison with other
models and the different size versions of this new model rank highly on the
HuggingFace OpenASR leaderboard.

Bravo!

* [Moonshine on GitHub](https://github.com/moonshine-ai/moonshine)
* [Moonshine v2 paper](https://download.moonshine.ai/docs/moonshine_streaming_paper.pdf)
* [OpenASR leaderboard](https://huggingface.co/spaces/hf-audio/open_asr_leaderboard) - e.g.: "usefulsensors/moonshine-streaming-medium".
* [Colab "get started" example](https://colab.research.google.com/github/moonshine-ai/moonshine-v2/blob/main/python/getting-started-with-moonshine-voice.ipynb) - run this with a Google account, for instance open this link in a Chrome browser.
