---
title: "Week 2 Of Recurse Center"
date: 2024-01-15T18:08:05+05:30
draft: false
---

Greetings! My name is Raghav, and I'm attending the Winter 2 batch of Recurse Center remotely from New Delhi, India. I just completed my second week. Here are my day to day logs of what I've been up to and my reflections of the week:

#### Day 1 - Monday, Jan 8th: Building the volitional muscles 🧠💪🏽

The day started with a Zoom chat with Kevin Galligan. Kevin is a Lisp programmer who holds a Ph.D. His research project focused on [error correction code](https://en.wikipedia.org/wiki/Error_correction_code). He's the only Lisp enthusiast I've found in my batch so far, and I look forward to pairing with him. We discussed his BitTorrent game project, how RuneScape Private Servers came to be, and, obviously, our love for Lisp.

Next on the agenda was the volitional muscle workshop. Building your volitional muscle is one of the three self-directives.
>Building your volitional muscles means growing your ability to make decisions about your work and learning based on your own curiosity and joy, rather than external pressures and fears. Your volition, or ability to make decisions and act on them, is something you can grow by exercising it, just like a muscle. 

Hosted by the RC faculty, Liz, we were asked to create 3 columns on a medium of our choice. The label for the first column was 'Ideas'. We had to write down every idea that crossed our minds to work on at RC.

The second column was 'Why?'. Here, we had to write down the motivations for wanting to pursue each idea. As I was writing the 'why's, I understood which things I wanted to focus on and which I would be okay skipping.

The third column was 'What to do'. Here, we had to prioritize what to focus on and say no to the rest of the ideas.

The purpose of this exercise was to favor things we genuinely feel excited about and deprioritize things we want to do for any other reason, such as peer pressure, following trends (Looking at you, NN: Zero To Hero), or increasing job prospects.

After the workshop, I had a much clearer understanding of the things I wanted to do over the next 12 weeks. The three main things I want to focus on are:
1. Finish the [Crafting Interpreters](https://craftinginterpreters.com/) book.
1. Learn Rust. Found a great resource created by another Recurser, Nicole. https://yarr.fyi/
1. Deep dive into Databases, preferably by implementing some of the concepts in Rust.
1. Build a personalized website.

I ended the day by going through the first chapter of the Crafting Interpreters book. The Introduction chapter mainly involved how the book is structured and what to expect out of it. I learnt about how some languages use tools like [Lex](https://en.wikipedia.org/wiki/Lex_(software)) and [Yacc](https://en.wikipedia.org/wiki/Yacc) to generate source files for compilers from a higher-level description (Grammar file).
There is a study group meeting coming up on Thursday.

#### Day 2 - Tuesday, Jan 9th

Someone reached out to me on Twitter regarding my [metronome app](https://accelonome.com) not functioning on mobile anymore. I made a change two weeks ago which broke it for small screens. [Fixed that](https://github.com/raghavio/accelonome/commit/b62980f272b5a2e5ebc7f07ff9f1b3d1194ae1d5).


I watched the talk [Making Hard Things Easy](https://youtu.be/30YWsGDr8mA) by Julia Evans. It was an insightful talk, in which she discussed strategies for understanding complex topics through tiny deep dives and implementing your own versions of them. More than the talk, I simply enjoyed her giggling about stuff every 20 seconds. It was both joyful and insightful, making it a must-watch for everyone.

Later, I was out meeting an old friend, so I joined late for the [SuperCollider](https://supercollider.github.io/) workshop hosted by Zach Scholl. It's extremely intriguing, especially since I've been interested in getting into algorithmic music composition. I definitely plan to spend some time exploring this in the coming weeks.

There was a Rust mob programming session happening for [Learning Rust With Entirely Too Many Linked Lists](https://rust-unofficial.github.io/too-many-lists/). I was told it's for people who haven't done a 'Hello World', but frankly, I didn't understand like 70% of the things. I'm hoping things will make sense once I start digging in the [Rust book](https://doc.rust-lang.org/book/).

Read half of Chapter 2 of Crafting Interpreters. Ideally, I should have completed it, but today was a lot. Chapter 2 discusses the various components and parts of language implementation. It briefly covers topics that are expanded upon in multiple chapters later in the book. Things like scanning, parsing, static analysis, IR, Tree-walk interpreters, and more.

#### Day 3 - Wednesday, Jan 10th: Creative Coding!

An eventful day.

I attended my first Zoom check-in. It's a daily event where you join a Zoom room and talk about what you did yesterday and your plan for today. It's similar to a daily standup at work, except this will not bore you to death and is completely optional. The question of the day was, 'What do you look forward to?' Since Delhi is super cold and gloomy these days, my answer was 'the Sun' ☀️.

Attended the [CryptoPals](https://cryptopals.com/) challenge event. It was refreshing to see people implementing the encoding schemes themselves. I haven't done any challenges yet though.

I reached out to Raunak for a coffee chat. Raunak is in the Winter 1 batch and is attending remotely from Mumbai. We spoke about our plans, how a WASM interpreter became his main project, and, most importantly, managing everything from the IST timezone. He affirmed that it's quite normal to feel all over the place during the first few weeks. It was also reassuring to know that I'm not the only one who planned something and is mostly doing something else here. 😅

I participated in the Creative Coding event. It's a weekly event where you're given a prompt to build something creative and expressive around it in 90 minutes. The prompt was "[Murphy's Law](https://en.wikipedia.org/wiki/Murphy%27s_law)".

My idea was the breaking of a guitar string. It's annoying, has happened to everyone who plays it, and truly captures that whatever can go wrong, will go wrong. For implementation, I forked someone else's [guitar fretboard app](https://1j01.github.io/guitar/) and messed it up. Here's a live demo of the app: https://raghavio.github.io/broken-guitar/

I attended the non-programming talks, a weekly event. There were 3 talks scheduled.

First up was Reed Spool, he spoke about his [e-ink mobile](https://hisenseeink.com/products/hisense-a9-pro-e-ink-smartphone-1) and a very interesting controller looking keyboard device, [Twiddler](https://twiddler.tekgear.com/). He demonstrated typing with it and was super fast. 60 WPM fast. With one hand. Crazy!

Next was Blaise Watson, he shared his experience cycling across the USA on the  the [TransAmerica bike trail](https://www.adventurecycling.org/routes-and-maps/adventure-cycling-route-network/transamerica-trail/). That's 6,800km. A distance greater than the length and breadth of India combined. It took him about three months. He took us through the journey by sharing a lot of pictures of the journey, what he ate, and his gear. It was all super inspiring. Made me think of buying a bicycle. Only to go to the gym though, nothing more than that. The title of his talk was 'Biking across America'. It was funny because for half of the presentation, until he showed the picture of his bicycle, I thought he was doing it on a motorcycle. It made sense how he was burning 10,000 calories a day.

The last speaker was Quinten Konyn, they spoke about similarities between [Dungeon Crawl Stone Soup](https://crawl.develz.org/) and RC. A very elaborate open-source game they've been playing since 2011. It was so nice to hear that they also made a contribution to it in 2019 related to the pronouns of NPCs.

I managed to finish chapter 2 of the Crafting Interpreters book. I'm looking forward to the study group tomorrow.

#### Day 4 - Thursday, Jan 11th: Presentations!

Started the day by attending the Zoom check-in. Today's question prompt was "What's your non food related favourite smell?" I love the smell of rain on dry ground. I even own a petrichor perfume ([Attar](https://en.wikipedia.org/wiki/Attar)).

Participated in the Crafting Interpreters study group, where we covered the first two chapters It was extremely insightful. I realized the potential of a study group as opposed to just doing it alone. I got to know a bunch of new things, some of the interesting being [loop unrolling](https://en.wikipedia.org/wiki/Loop_unrolling), [Duff's device](https://en.wikipedia.org/wiki/Duff%27s_device), and the fact that [all browsers in iOS is just Safari??!](https://news.ycombinator.com/item?id=25850091)

I had a long, fun and relaxed call with Jatinderjit from the Winter 1 batch. He's based in Bangalore but was joining from Firozpur, Punjab. We discussed startups, programming languages, giving up on SICP, and the desire to study databases internals.

Ended the day by attending the weekly presentations event. You get 5 minutes to give a presentation about what you've learnt at RC. Julie Bodian, showed her MIDI Visualizer project. It reminded me of those WinAmp and Windows Media Player animations. Zach Ahn talked about his Safari extension which replaces reddit.com URLs to old.reddit.com. And a couple of more cool presentations.
The entire atmosphere was so welcoming. The presentations, the clapping afterward, and the brilliant monologue by Liz talking about the RC culture and self-directives. I felt privileged to be around such amazing people doing even more amazing work.

#### Day 5 - Friday, Jan 12th: Rust And Relax

Mostly a chill day again, but I started learning Rust!

During the Zoom check-in, we had a quite thought-provoking question today: 'How long will you survive in a Zombie apocalypse?' I think I've played enough Left 4 Dead to survive at least a week. My confidence only increased after hearing others' responses. At this point, I sound like the person who thinks he knows everything and is the first to die in the group.

☕ chat with Divyendu. He's attending from Berlin, Germany. We discussed our time at RC, his file compression project, how annoying Haskell jargon is, and how Delhi winters feel extra colder. He had an interesting approach where he frequently deep-dives into a new topic for a day or two to see if he would like to stick to it.

I finished two chapters of the Rust book. Things are a bit confusing but so far so good. Through the book, I found out about [Semantic Versioning](https://semver.org/). Eagerly looking for some projects to practice Rust on.

Weekend is here, and I plan to finish blogging both Week 1 and Week 2's updates.

### Reflections

I wasn't very productive, but I'm happy with the progress I made this week. I finished two chapters of the Crafting Interpreters book and started learning Rust. I spoke to a lot of cool people and watched some interesting presentations. 

I also did a bunch of other things that I can't quite quantify, like browsing Zulip and going through others' check-in logs. One might think that's a distraction, but I don’t. It's really like a mini-adventure. From geeky Formal Methods talk to the creative possibilities of OpenGL Shading, from Bret Victor's groundbreaking ideas to Applied ML, and sometimes, it's all about [cracking codes](https://cryptopals.com/) in Cryptography. It's not just scrolling; it's learning and realizing the incredible diversity of the RC community.

Next week, I'm excited to level up on Rust and get to the coding part of the Crafting Interpreters book.
