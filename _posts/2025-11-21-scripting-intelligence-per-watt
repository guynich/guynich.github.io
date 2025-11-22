---
layout: post
title: "Hazy Research: Intelligence per Watt study"
date: 2025-11-21
---

[Hazy Research](https://hazyresearch.stanford.edu) is a computer science
research group at Stanford University led by Professor Chris Ré.  I do like the
name!

Earlier this year I was inspired by the group's
[Minions](https://github.com/HazyResearch/minions) project and I contributed
three commits to that repo and ran some experiments of my own with this
exciting framework using a low power ARM CPU.

Professor Ré starts a
[May post on the group's blog](https://hazyresearch.stanford.edu/blog/2025-03-25-ai-usa)
by saying "We’ve been given a machine that turns energy into intelligence".  So
I was fascinated this week to read about the group's new
[Intelligence per Watt study](https://hazyresearch.stanford.edu/blog/2025-11-11-ipw).
I think this is very timely.

I've
[installed the code](https://github.com/HazyResearch/intelligence-per-watt)
on my Linux workstation with an older NVidia GPU and it's running as I write.
The NVidia utility reports my GPU is using 65 Watts and the profiling test
looks like it will take 1 hour and 20 minutes to run 1000 prompt queries with a
small version of Meta's Llama 3.2 large language model.

I can't provide a reference but I once heard that a human brain might use
energy equivalent 25 Watts of electrical power.  This might infer the profiling
test on my GPU equates to asking three humans to each provide answers at a rate
of around 250 text questions in one hour, or around 4 questions per minute.
That seems a gruelling task to me!  Anyway a fun (if imperfect) comparison.

It's interesting, though probably unsurprising, the
[study quantifies](https://hazyresearch.stanford.edu/blog/2025-11-11-ipw)
Apple's M4 silicon providing significantly more intelligence per watt than
earlier NVidia GPU architectures.  I'll see if my older GPU lands close, but
predict not.

I'll try and see if I can get this to run on small Raspberry Pi like boards as a
next step.

Well done Hazy Research for putting this out.

===

PS: I've been very hands-on with a project that's required **a lot** of bash
scripting on macOS.  I hadn't appreciated quite how ancient is the bash version
that ships on macOS.  Luckily
[brew](https://formulae.brew.sh/formula/bash) and
[MacPorts](https://www.macports.org)
both provide up to date bash versions that have been helpful.
