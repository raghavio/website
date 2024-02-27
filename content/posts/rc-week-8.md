---
title: "Week 8 Of Recurse Center"
date: 2024-02-25T18:05:23+05:30
draft: false
---

It's a bit crazy to think that by the end of this week, I'll have been here for two months.

#### Day 1 - Monday, Feb 19th

Started the day by doing the snail rustlings with the usual gang and Ludwig Schubert. He was very helpful with some of the Rust concepts, and in between, we got to see his plotted patterns. You ought to check them out in his check-ins.

I got back to reading Chapter 8. After spending an awful amount of time implementing [this](https://github.com/clojure/core.match) Clojure pattern-matching library in my code, I figured it didn't even make any sense for my use case.

I also read [why](https://gist.github.com/reborg/dc8b0c96c397a56668905e2767fd697f#why-no-pattern-matching) Rich Hickey dislikes pattern matching and why it's not built into the core Clojure library. Also, that document is pure gold!

After a couple of hours, I finally [wrapped up](https://github.com/raghavio/crafting-interpreters/commit/fe2b248feb1743e4bd931ea8f932ec8a794db0a8) the Chapter 8 implementation. I took a different approach to managing environments and scope than what's suggested in the book. Instead of resorting to silly mutations and creating new class objects for each scope's environment, I went for a simpler and more efficient approach. I'm passing the environments in each "visitor" function, and recursion takes care of the scope. The book does mention this approach, but it would've been too verbose in Java. Makes sense to save pages in a book.

✨ Emacs ✨ stuff. I got to know about lsp mode and a bunch of cool packages from Aditya's [blog](https://www.evalapply.org/posts/emerging-from-dotemacs-bankruptcy-ide-experience/). This was especially helpful as it's tailored for Clojure development. Now, I just need to figure out whether I should use eglot or lsp-mode. I'm a bit unsure about the differences at the moment.


Some highlights as I was lazy around the last few days. I've made my peace with it now. I remind myself that I'm actually on a sabbatical and it's okay to just do nothing or chill sometimes. Not all days can be productive.

#### Day 2 - Tuesday, Feb 20th

I had a wonderful chat with Shae Matijs about Emacs. I was in awe of hearing him talk about Emacs and his setup. It just got me so excited to diligently learn it. He has been using Emacs for 25 years! He got his email, calendar, Twitter, terminal, etc., all inside Emacs.

A lot of folks who advocate Emacs particularly cite how it's light, fast, and uses less RAM, but I guess he didn't have to worry about any of that considering his Thinkpad P\<something> was a beast with 120 GB of RAM and a multi TB disk 🤯. I honestly didn't know laptops came with that much RAM. He had a custom setting that pops up his org agenda list after his system stays idle for 30 minutes. The first thing you see once you come back to your system is your TODO list. That's so neat!

I got to know about [ripgrep](https://github.com/BurntSushi/ripgrep) from him, a recursive grep library written in Rust. DoomEmacs is awesome because all the packages he spoke about already come with it.

After the call, I started reading Chapter 9 of Crafting Interpreters. It is about control flow statements, and we will implement the if block and while/for loop in it. A small one compared to the last chapter.


#### Day 3 - Wednesday, Feb 21st

The creative coding prompt was 'Go to an extreme, move back to a more comfortable place'. After quite a bit of pondering, it made me think of job hunting and interviews. How the interviews are always on the extreme end but the work afterward not so much. [This tweet](https://twitter.com/TheJackForge/status/1760672776359440442) perfectly captures what I mean. 
I decided to mimic the Leetcode interview round. An online code editor where you're asked to finish inverting a binary tree. After successful submission, you get an alert saying "Congratulations! You can get comfortable now and center a div.". I forked a JS playground and made some changes to the app.
![](/creative-coding-feb-21.png)

#### Day 4 - Thursday, Feb 22nd

I had a pairing session scheduled with Kevin. He wanted to do some reverse engineering, and his idea was to view the network traffic of online games and tamper with it locally. We picked Chess (Lichess) since we both play it. Lichess uses Websockets for communication. After figuring out the payload, we tried sending our own requests to the connection, and it was working fine. We also tried to make some illegal moves, but those messages got ignored, obviously.

After that, we thought of an idea to be able to make moves by entering positions in the chatbox. Like "g8f6" would move the piece on g8 square to f6. To do this, we had to scan for the messages in chat, fetch a valid position using regex, and trigger that move via WebSocket request.

For the first step, we used [MutationObserver](https://developer.mozilla.org/en-US/docs/Web/API/MutationObserver) interface. It lets you track changes made to the DOM. Here's the code we used:
```javascript
const observer = new MutationObserver((mutationsList, observer) => {
    for(const mutation of mutationsList) {
        const move = mutation.addedNodes[0].innerText.match("[a-h][1-8][a-h][1-8]")[0];
        console.log(move);
        makeMove(websocketObj, move); 
    }
});

observer.observe(div_section, { 
    attributes: true, 
    childList: true, 
    subtree: true }
);
```

This looks good, but there was one problem. A problem that Kevin decided to keep to himself. We are not doing any validations for who is sending the message and whose turn it is. As soon as I evaluated that code, Kevin sent a message in the chat, which triggered a move on my behalf. He moved my queen and captured it using his bishop. Gaaah!

I had a lot of fun in this pairing session.

After the session, I quickly finished reading Chapter 9 of Crafting Interpreters before the study group. It was a relatively straightforward read. In the study group meeting, we discussed dynamic scoping, the grammar of if blocks and the dangling else problem, bash's absurdity, and tail call optimizations.

After the meeting, I got curious to know how functional languages handle TCO in JVM since it doesn't support TCO due to security reasons. It messes up the stack frame. Clojure and other languages use an explicit keyword to let the compiler know that the function needs to be optimized for tail call recursion. This code then gets transformed into Java's while loop. Clojure has `recur` and Kotlin has `tailrec`.

#### Day 5 - Friday, Feb 23rd

I went out for the hangs and was extremely tired when I got back home. So, no work.

#### Weekend

I went to a 2-day music festival in my city and saw some great artists, particularly my favorite jazz pianist, Tigran Hamasyan. It was such an experience to catch him live, even though he didn't play my [favorite song](https://youtu.be/-VOZLG-FlvI).