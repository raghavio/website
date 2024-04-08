---
title: "Week 6 Of Recurse Center"
date: 2024-02-12T22:13:42+05:30
draft: false
---

It's been 6 weeks. Nobody told me time flies here. It's the end of the batch for Winter 1, and I'll miss those folks. I hope they stick around for a bit. I slumped with journaling this week due to many factors. Hence, this post will be short.

### Day 1 - Monday, Feb 05th

Coffee chat with Shannon Werle. We discussed our time at RC, working at a small startup vs. a big company, and worker cooperatives.

I moved my Lox implementation to a [Clojure app](https://github.com/raghavio/crafting-interpreters/blob/main/clojox/test/clojox/core_test.clj). I'm still using the Java Scanner code, thanks to interoperability. No more visitor pattern though!

Thought about an app to practice my Rust: a Pomodoro tracker/reminder TUI (or CLI) that pauses notifications during focus time and enables them back for break time. Maybe also send reminders every few hours to journal, drink water and eat meals.

### Day 2 - Tuesday, Jan 07th

Started with the Zoom check-in. The QOTD was 'Would you rather come early or leave late?'.
Those who know me can attest that, forget to come early, I can't even manage to come on time.

I researched the expression problem and various ways to solve it. In Lisp languages, you can use multimethods, which offer a simple and powerful approach to runtime polymorphism. You specify your dispatch criterion and write a function that it should dispatch to if the criterion is met. There are also Clojure protocols, they are fast but are limited to class dispatch. For my interpreter, I'll be using multimethods.

Chris and I joined Dan at a pairing station, where he discussed the [TypeScript bug](https://github.com/microsoft/TypeScript/issues/16069) he's trying to fix—a bug he filed himself some 7 years ago. I was fascinated because it seemed daunting to fix, probably why no one bothered fixing it for 7 years. He was kind enough to explain the issue, how he approached it, and where he was stuck. I managed to understand most of it, so he did a stellar job. Thank you, Dan!

Looking at compiler code is funny. It's the opposite of all the good software practices you're told about. You'll find functions spanning over 1000 lines, [50k-line files](https://github.com/danvk/TypeScript/blob/2b040f3b8fc85435e83fd25663877eb795d6379b/src/compiler/checker.ts) that GitHub refuses to open, lines stretching a few hundred characters in length, and barely any comments. But, I'm sure they are trying to save every nanosecond. They obviously know what they're doing.

I'm finished going through Chapter 6 of Crafting Interpreters. I'm yet to do the code implementation though which I'll be doing today!

## Reflections

This week was a bit overwhelming, both at RC and outside, which resulted in me stopping journaling and checking in. I'm not proud, but it is what it is. I picked up a lot from the reflections call, thanks to all the lovely folks who shared their introspection. I look forward to implementing some of the advice, mostly from Will on meditation and setting the day. I also missed the Crafting Interpreters meeting, but I finished my [interpreter implementation](https://github.com/raghavio/crafting-interpreters/commit/ffa3e4e79ecde27cb1b4c2e1f9abacf0f1a2f658) over the weekend.
