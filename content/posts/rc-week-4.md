---
title: "Week 4 Of Recurse Center"
date: 2024-01-30T18:44:46+05:30
draft: false
---

Week 4 was all about diving into Rust, tinkering with Java to write a programming language scanner, and some cool group sessions. I got my hands dirty with Rust's memory model, Java 21, and explored some of Bret Victor's ideas.

### Day 1 - Monday, Jan 21st:

Rust makes me feel like learning to program for the first time. 

- Mini mob programming session with Shaq and Thomas. We did exercises of yarr.fyi's memory section. We were all confused but we made it through. I'd love to continue. It might be better if we can also find someone who already understands a little bit of Rust.

- Enjoyed the Twitch/coop/not a mob/ game programming session by Quinten and Reed. We experimented with Rust's [nannou](https://nannou.cc/) library.

- Attended the Bret Victor reading group since everyone is always talking about it, and I get the vibe. This session was a show and tell where people demoed interactive web designs that aligned with Bret Victor's philosophy (I think). I haven't seen any of his talks or read any essays yet, but hopefully, I will this week.

- I decided to do Crafting Interpreter in Java. It's been a decade since I last wrote in it, and all the new updates in Java 21 look interesting. I set up the VSCode. Read a bit of Chapter 4.


### Day 2 - Tuesday, Jan 22nd:

It was a very head-down, focused day. I finished Chapter 4 of Crafting Interpreters in Java. I'm trying my best not to straight-up copy paste the code from the book. Although my functional brain wants to do things I shouldn't be doing in Java, I keep telling myself that classes are there for a reason and mutation is okay (ugh).

Chapter 4 also has a tiny bit of theory around [regular language](https://en.wikipedia.org/wiki/Regular_language), [Chomsky hierarchy](https://en.wikipedia.org/wiki/Chomsky_hierarchy) and finite-state machines. Did not really understand any of that tbh. I'll bring it up in the study group.

### Day 3 - Wednesday, Jan 23rd:

- Coffee chat with Gunjan Tank. She's joining in from Bangalore. Other than the usual tech stuff, we spoke about her Vipassana experience and how I too almost participated once but got scared. For the uninitiated,  [Vipassana](https://www.dhamma.org/) is a strict 10 day meditation retreat that has centers worldwide.

- Createive Coding prompt was "Impossible objects (undecided geometry)". I was blank, so decided not to make anything, but loved what others built. There were a bunch of cool projects!

- Made some enhancements to my Scanner code for jlox. [Here's](https://github.com/raghavio/crafting-interpreters/tree/main/jlox) the Github repo.

- Read this blog about the difference between Rust references and pointers.

- I came across another Rust resource by Brown University. It's an enhanced version of the Rust book. I plan to go through the [ownership chapter](https://rust-book.cs.brown.edu/ch04-01-what-is-ownership.html) in it.

### Day 4 - Thursday, Jan 24th:

- Crafting Interpreters study group. I didn't know we were discussing Chapter 5 🙈. I need to catch up. I didn't understand much of the discussion, but it was still fun. It was cool to see TypeScript's [Scanner](https://github.com/Microsoft/TypeScript/blob/main/src/compiler/scanner.ts#L1786).It's huuuge, but the structure feels similar to what's there in the book, and I'm happy how I can kind of make sense of things.

- I spent some time reviewing the challenge answers at the end of the chapter, provided by the author himself, Bob Nystrom. [Here](https://github.com/munificent/craftinginterpreters/blob/master/note/answers/chapter04_scanning.md) they are.

- Attended the presentations. I feel like every single one was mind-bogglingly cool. It's always so fun to see what cool stuff people are building!

- There was a Staff+ Engineer roundtable event that I really wanted to attend but my Zoom said enough for the day.

### Day 5 - Friday, Jan 25th:

- Paired (?) with Reed Spool. He's developing a Forth interpreter in C for Playdate. I wasn't familiar with any of those things, but he was kind and patient enough to explain them. Forth is... interesting. It reminded me of REPL and macros, so we discussed how it differs from Lisp. In the end, we tried to debug some of the compiler warnings. Although I couldn't contribute much, I was happy to know more about Forth and C.

- Attended an event on building TUIs with [Ratatui](https://github.com/ratatui-org/ratatui). We made a Hello World TUI app and saw some cool demos.
