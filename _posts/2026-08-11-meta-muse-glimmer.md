---
layout: post
title: "Meta's Muse Glimmer model - smoke testing"
date: 2026-08-11
---

TLDR: Muse Glimmer is slower than my local coding agent baseline

Company Meta's announcement yesterday:
[Introducing Muse Glimmer: An Open Agentic Model That Runs on Your Device](https://research.meta.ai/blog/introducing-muse-glimmer-open-agentic-model).

I was curious to swap out the Qwen 3.6 model with Muse Glimmer in my
[local-coding-agent framework](https://github.com/guynich/local-coding-agent).

Test environment
* MacBook Pro (M5 Pro, 48GB)
* Ollama version 0.32.8
* Ollama model tags:
  * `muse-glimmer:30b-mlx`
  * baseline: `qwen3.6:35b-mlx` [with modified sampling parameters](https://github.com/guynich/local-coding-agent/blob/main/coding_model.md)

First I ran
[Sebastian Raschka's benchmarking script](https://magazine.sebastianraschka.com/i/203767454/4-simple-speed-performance-assessment)
and saw Muse Glimmer run more than **3x** slower at around 20 tokens per second.

I then asked it to run a repo code review for a macOS/iOS app I am developing.
After 10 minutes of thinking the Qwen Code API timed out.  I'll try later to see
if Ollama implementation of Muse Glimmer runs faster.

Conclusion: I'll stick with the Qwen model for local coding work.
