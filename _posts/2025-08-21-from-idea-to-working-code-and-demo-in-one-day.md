# From Idea to Working Code & Demo in One Day

Earlier this week, I set myself a challenge: to go from a blank page and an idea to a working demo, complete build process, and a pull request (PR) to an open-source GitHub repository — all in one day.

The existing repo [ten-vad](https://github.com/TEN-framework/ten-vad) provides a promising new ML model for voice activity detection (VAD), which helps speech recognition systems more accurately detect when someone is speaking. The repo is written in C and includes a working demo. However, many users prefer working in Python. One existing project attempted a full Python reimplementation of the C library, but it doesn't yet replicate all the original functionality, and its numerical results may differ.

Instead, I took a different approach: building Python bindings to wrap the original C library. This allows Python code to directly import the new extension module and access the original C functionality via a clean, Pythonic API.

All within one calendar day <sup>1</sup>.

I had to work with tools I’m not deeply familiar with — like CMake build scripts and Python binding techniques. To help with that, I turned to an AI code editor called [Cursor](https://cursor.com). With its help, I went from a blank slate to a working, tested PR in under 24 hours — something that might’ve taken me five or more days on my own (though it’s hard to say exactly).

I wouldn’t call this “vibe coding” — a term I’ve seen used for casual or exploratory work. “Assisted coding” feels more accurate. Cursor handled the workflow impressively — diagnosing bugs in both the build process and my suggested changes, then implementing fixes and generating creative tests. I’ve used Cursor for nearly a year, and its recent ability to write and run test cases — and then automatically fix and validate issues — has been a major productivity boost.

Building cross-language libraries is complex work. As the 24 hour mini-project came together, I asked Cursor to run end-to-end tests comparing my Python demo to the existing C demo in the repo. That freed me to focus on code structure and architectural improvements. I could review the test results and use them to guide design decisions.

The tests confirmed that the model's prediction results in Python matched those of the C demo. The Python version does run slower — unsurprising, especially when looping with constructs like `for` loops.

I'm genuinely appreciative of how these tools accelerate development. What might have taken me five or more days of learning, coding, and testing was completed in a single day.

Here is my PR with build script, documentation, and test results:
[https://github.com/TEN-framework/ten-vad/pull/61](https://github.com/TEN-framework/ten-vad/pull/61)

It’s fascinating to see how businesses and computer science students are rethinking development workflows with tools like Cursor. I’m excited to keep learning and building more with them.

<sup>1</sup> In the 24 hours, apart from coding and testing, I got more than six hours sleep plus went to a theatre production of Shakespeare's Twelfth Night.  *If music be the food of love, play on ...*
