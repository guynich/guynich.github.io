---
layout: post
title: "Google's multimodal LLM model, good old BART and a new Tinker."
date: 2025-10-03
---

Continuing on from my
[last post](https://guynich.github.io/2025/09/18/neural-codecs-and-small-llms.html)
on neural codecs with LLMs, e.g.: audio interfacing, I've tried a "multimodal"
LLM called `Gemma3n`.  It can take text, audio or images as input, and
generates text in response.  I'm assuming the Gemma3n model has an internal
neural codec to tokenize the raw audio - probably a version of Google's
Soundstream.

I adapted Google's
[audio understanding example from gemma-cookbook]()
to make a standalone Python version in
[my GitHub repo](https://github.com/guynich/audio_understanding).
Functionally it is identical, re-using the same input audio and demonstrating
the same generated result.  Along the way I spotted a bug in Google's example
and submitted a code change in this
[pull request](https://github.com/google-gemini/gemma-cookbook/pull/242)
to fix it.  Thanks to @bebechien for the review and merge!

I hit memory allocation issues trying the model on a MacBook Air M3 with
16GB RAM (24GB RAM should work better) so I switched to an Intel Xeon
workstation with 48GB RAM and ran the model without any GPU.

Here's the application changing a shopping list based on user speech
instructions in several audio files.

```console
----------------------------------------
user:
itemize it into a shopping list.
user audio: shopping1.wav

assistant:
Here's your shopping list:

* 1 milk
* 3 apples
* 1 tofu

user audio: shopping2.wav

assistant:
Here's the updated shopping list:

* 1 milk
* 4 bananas
* 1 tofu

user audio: shopping3.wav

assistant:
Here's the updated shopping list:

* 1 milk
* 4 bananas
* 1 tofu
* 1 dozen eggs
```

Working hands-on with an LLM that can take raw audio as input is cool and I
was impressed with this example and other results from this LLM.

===

Separately I ran a project that runs daily text summarization from some RSS
feeds. Initially I ran some quick tests with a small quantized version of
Google's Gemma 3 LLM to do the text summarization.  I found the resulting text
summary not as readable as I would like and, despite my prompt request to keep
a URL, the generated text did not include any click-through URL links.

Instead of Gemma 3 LLM I used an older model called
[bart-large-cnn from Huggingface](https://huggingface.co/facebook/bart-large-cnn)
in my project.  This change immediately delivered useful text summaries with
the wanted URL links.  It also runs fast enough on CPU for my use case.  Good
stuff that works.

===

A new product announcement this week called
["Tinker" by Thinking Machines Lab](https://thinkingmachines.ai)
got my attention.

This is an application programming interface (API) to enable fine-tuning of
large language models.  I
[mentored a project team for the R42 Institute](https://guynich.github.io/2025/08/19/mentoring-an-ai-fellow-summer-project.html)
this summer on a similar topic.

The approach in the "Tinker" documentation makes sense.  It hints that
fine-tuning is not easy and states the API is not a magic black box.  Instead
the product lets the user focus on the task specification, dataset and
validation - allowing the user to avoid owning the complex engineering needed
to fine-tune models.  I'll be following Tinker developments.
