---
layout: post
title: "An honest take from Cloudflare on AI and open source contribution"
date: 2026-08-07
---

This snippet from the [cloudflare-os contributing
guidelines](https://github.com/cloudflare/cloudflare-os#contributing) caught my
eye:

```text
AI has made writing code easy. The hard part, today, is not writing the code,
but reviewing it, making sure quality stays high, and keeping the product
coherent.
```

Cloudflare has closed cloudflare-os to outside contributions for now, with one
exception: small, "trivially-verified" PRs under about a dozen lines that fix a
real problem. Typo fixes and anything larger get closed with a link back to the
policy.

What stands out is the reasoning, not just the rule. As they put it, external
contributions in the AI era risk "donating" the easy part of the job —
generating code — while dumping the hard part, review and quality control, back
on the maintainers. That's a pretty direct acknowledgment that AI coding tools
have shifted the bottleneck in open source from writing to reviewing, and that
the usual PR-welcoming posture doesn't automatically make sense anymore when
anyone can generate a plausible-looking diff in seconds.

It's a small policy note, but it says something bigger about where maintainer
effort is going to be spent going forward.
