---
title: "Week 9 Of Recurse Center"
date: 2024-03-05T15:32:54+05:30
draft: false
---

Okay, check-ins feel like a chore now. 

My energy levels have been low this entire week. I haven't done any coffee chats or pairing sessions, and my online social battery has been depleting week by week. As the batch is nearing its end, I feel more inclined to finish up some of the things I had planned: Part 1 of the Crafting Interpreters book, learning Rust by building Redis, and creating a personalized website. Consequently, I have zero desire to join some otherwise interesting events, but let's see if I feel differently this week.

Some highlights from last week: 

I [finished implementing](https://github.com/raghavio/crafting-interpreters/commit/fef0adee26d953f9b8004b33e0c98e2fa5411ee8) the control flow statements for my interpreter, which now includes `if`, `while`, and `for` loops! While working on that, I encountered a bug in my Environments code related to scoping, necessitating a refactor to fix it. In the Crafting Interpreters group, we covered Chapter 10, focusing on Functions. Super excited to implement that and the next chapter this week.

Came across [Jank](https://jank-lang.org/), which is a Clojure dialect on llvm and watched this super informative [video](https://youtu.be/Yw4IAY4Nx_o?feature=shared) on building a Clojure dialect.

The presentations were fantastic as usual, but the highlight for me was Jake Feintzeig's [presentation](https://docs.google.com/presentation/d/1KJxhvVI6PKQFi07DK-Rjm6v1gddtKuqAQ12EnctGAZA/edit#slide=id.p) on optimizing a ray tracer. The image he generated took more than 3 hours, and his talk was a deep dive into compiler optimizations to make it 130 times faster, particularly focusing on the -O2 optimization flag in gcc. He compared the disassembly with and without the flag to understand how it works and why. This was incredibly inspiring and fascinating. My brain is so accustomed to generating shareholder value that I would have been content with just discovering the flag and moving on with my life. However, that's the beauty of Recurse Center for me - to be more curiosity-oriented than strictly output-focused. It will probably take me another retreat to get there 😝.

I've been thinking of ideas for my personal website lately. Right now, it's just a boring, ugly Hugo blog. I want to create something that reflects me – my style, my hobbies, the music I like, the music I create, my plants, my terrarium, my desk, and more. I'm still in the process of figuring out how to represent all these aspects in code, but my current plan is to create a masonry-style picture grid as a background. Let me know if this interests you and if you'd like to brainstorm ideas.