---
title: "Week 5 Of Recurse Center"
date: 2024-02-05T21:14:37+05:30
draft: false
---

### Day 1 - Monday, Jan 29th:

Week 5! 1/3rd of the batch is over. Can you imagine?? wtf

Coffee chat with Christopher. We discussed distributed systems, Paxos, and Raft.

Coffee chat with Zack Scholl. We discussed our music projects and programming languages. It was fun to see the progress of his hardware project and its user interface. He also had some wicked ideas to make [my metronome app](https://accelonome.com/) distributed. I learned about [Orca](https://hundredrabbits.itch.io/orca), an esoteric programming language to write MIDI. We also spoke about the backward compatibility of programs and languages, which reminded me of this classic Rich Hickey [talk](https://www.youtube.com/watch?v=oyLBGkS5ICk) on that subject.

I published Week 3's blog. 🙄

Found out about the [Zed](https://zed.dev/) text editor, built by the makers of Atom. They recently open-sourced it. Looks promising, but I couldn't try it as it's only available on Mac for now.

Tried making sense of Context-Free Grammars in Chapter 5 of Crafting Interpreters, but failed.

### Day 2 - Tuesday, Jan 30th:

I was struggling with the theory around Formal Grammars, and thankfully, I wasn't the only one. Umair and Blair were discussing Chapter 5 at a pairing station, and I decided to join them. After spending 5 minutes trying to figure out the Zoom whiteboard, we switched to Excalidraw to understand the grammar-to-AST transition. It definitely helped, but I was still mostly confused. Things began to click a bit more after re-reading parts of the chapter and watching [this Computerphile](https://youtu.be/224plb3bCog) video on the Chomsky Hierarchy.

Lately, my productivity has been in the dumps, so I've started journaling my day in an actual, physical notebook. So far, so good. I'm jotting down everything – wake-up time, how long I laze around in bed (aka the 'hurkle-durkle' time), my to-dos, meal times, updates on what I'm doing every few hours, and even my daily phone screen time. The plan is to guilt-trip myself into reducing the negatives each day. Plus, I'm doing it all on this fancy, handmade paper which apparently takes a whole day to make. It kind of makes me feel obliged to finish the to-dos, out of respect for the paper makers.

### Day 3 - Wednesday, Jan 31st: Recurse metal song!

I went to the Zoom check-in after a while. The QOTD was choosing between Telekinesis or Telepathy. As much as I like gossip and nosing around, I chose Telekinesis. Reading other people's thoughts would be too intrusive, and also, no one would want to be my friend 😔.

After that, I attended the Volitional And Career workshop. The questions were thought-provoking, and I enjoyed writing the answers to them. I got to meet some amazing folks in the Zoom breakout rooms, and it was inspiring to hear their stories and their plans for the future.

For Creative Coding, the prompt was "Generative music". I wasn't feeling like writing any code and I've been meaning to try some of the music-making AIs. I used [Suno AI](https://www.suno.ai/) and the outcome was mind-blowing. After a bunch of trials in different genres and with different lyrics, I ended up finalizing a heavy metal song with Metallica-inspired lyrics on Recurse Center. Insane what you can do with AI these days.
https://app.suno.ai/song/8fd067fa-c893-4896-ba04-81dd299a48a5/
```spoiler Lyrics
[Verse]
In the realm of code, where minds ignite,
Browsing Zulip in the fading light.
Check-in logs, a path to find,
In Recurse Center, the tech entwined.

[Chorus]
Dive into the code, where secrets lie,
In the heart of RC, beneath the sky.
From Formal Methods to ML's flight,
We're cracking codes in the dead of night.

[Outro]
A mini-adventure in every line,
Exploring the depths where the tech stars align.
In this community, diverse and bold,
We're crafting the future, uncontrolled.
```

Later, I joined Will, Shaq, and Alex to do [Rustlings](https://rustlings.cool/). We all did the solutions on our systems and made some decent progress. It was great to do this in a group because it would've been quite boring otherwise. 

Not many people know, but listening to [this](https://www.youtube.com/watch?v=Ti_imhKBjXA) in the background while trying to understand Rust has a 100% success rate. If not, well, you end up with two solid reasons to headbang.

Right after Rustlings, I went to watch some non-programming talks. I loved Zack Scholl talk on [The Zen of Running](https://www.goodreads.com/en/book/show/336390). The presentation slides were crisp and beautiful 🤌🏼. I'll make sure to keep coming back to them every time I look for some inspiration to run.

Finally finished Chapter 5 of Crafting Interpreters. I'm still a bit clueless. I'm pretty sure I don't understand the visitor pattern very well. I'll see if it can be removed. Otherwise, I'm quite happy with my [Java code](https://github.com/raghavio/crafting-interpreters/commit/90e63d18e2a57dc7792be0b26e3ddc8647a11a3d#diff-52df63a8c062026fad82a32c373044ecd78385aa49e971f3f61c1808e435b754). It's much more concise than what's there in the book.

### Day 4 - Thursday, Feb 1st: Crafting Interpreters

Attended the Crafting Interpreters study group. I forgot what we discussed but it was interesting. Also, I'm like wayy behind. I **have to** wrap up Chapter 6 and 7 this week. Over the weekend, I realized life is too short to be willingly writing Java. I'm considering to move my jlox implementation to Clojure.

I had a Lovely coffee chat with Thomas Kelly. We discussed a bunch of topics. His time in India, Cricket (He doesn't follow it), Games, OOP vs Functional approach and our struggles with Crafting Interpreters. It's always so fun talking to folks who don't come from a traditional computer science background.


### Day 5 - Friday, Feb 2nd: Rust and Redis

I paired with Raunak on my jlox implementation. We tried some ways to avoid using the visitor pattern for forming the AST.

Later I thought of an idea to make a Pomodoro/reminder tracker app as a TUI in Rust.

Read the [slides of Rust lecture](https://web.stanford.edu/class/cs242/materials/lectures/lecture11.pdf) from [CS242 course](https://web.stanford.edu/class/cs242/coursework.html). Quite a clear demo of the ownership and borrow model. I also got to know that ownership isn't a new concept.

Made some progress on the [Build Your Own Redis](https://app.codecrafters.io/courses/redis/overview) course. It's pretty fun!