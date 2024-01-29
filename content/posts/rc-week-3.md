---
title: "Week 3 of Recurse Center"
date: 2024-01-21T02:17:13+05:30
draft: false
---

Week 3 was filled with a variety of programming and non-programming activities. Notable experiences included creating a Tic Tac Toe game in Clojure, discovering a new Rust resource, attending a TIC-80 workshop, and a very cool Creative Coding project.

For Creative Coding, I developed a game to demonstrate integer overflow, based on the Sisyphus myth, showing Sisyphus perpetually pushing a boulder uphill. 

Additional activities included coffee chats discussing programming and personal experiences, a chat on worker cooperatives, and attending the local PyDelhi meet-up to pick up my forgotten water bottle.

The week was a blend of learning, collaboration, and exploration of new concepts.

#### Day 1 - Monday, Jan 15th: Tic Tac Toe in Clojure

- Finished blogging about the updates for both weeks.
- Paired with Jenkhai Yew, courtesy of the pairing bot. We weren't sure what to work on together, so we chose one of the RC pair programming tasks. We created a basic, barely functioning Tic Tac Toe game in Clojure with no validations. Here's the code on repl.it. It was great to work with him. He was surprisingly quick to pick Clojure. I also loved his background. High school competitive coder turned literature grad turned programmer.

    ```Clojure
    (def winning-patterns
    [[0 1 2] [3 4 5] [6 7 8] [0 3 6] [1 4 7] [2 5 8] [0 4 8] [2 4 6]])

    (def board (vec (repeat 9 nil)))

    (defn check-for-winner
    [board]
    (some (fn [pattern]
            (let [values-for-pattern (mapv board pattern)
                    match? (apply = values-for-pattern)]
                (when match?
                (first values-for-pattern)))) winning-patterns))

    (defn set-board
    [board index value]
    (assoc board index value))

    (defn start-game
    []
    (loop [board board
            player0? true]
        (mapv println (partition 3 board))
        (println "Enter index to mark for " (if player0? 0 1))
        (let [new-board (set-board board (Integer/parseInt (read-line)) (if player0? 0 1))
            game-over? (check-for-winner new-board)]
        (if-not game-over?
            (recur new-board (not player0?))
            (println "You won!")))))

    (start-game)
    ```
- Discovered Yet Another Rust Resource and I think I'm going to go ahead with it instead of the Rust book.
- Attended the [TIC-80](https://tic80.com/) 101 workshop. I want to learn it for creative coding.
- Started the 3rd chapter of Crafting Interpreters.

#### Day 2 - Tuesday, Jan 16th: Impossible Day

- Coffee chat with Felix Caraballo. We mostly discussed Rust and Zig and how we hate reading a giant book to learn programming languages. He was kind to show and explain the Zig code from his midi controller project. It got me curious and I spent some time to better understand `comptime` and `inline` features of Zig.

- Researched for the impossible project for the Impossible Day. I've been wanting to learn more about distributed systems. Some of the ideas are to make a distributed KV store, or read the RAFT paper and eventually try to make one at some point. None of these aligns with my immediate goals, which are learning Rust and finishing Crafting Interpreters, so I'm still figuring out if I even want to attempt anything or not. Maybe I'll try to finish the Scanner chapter of the CI book in Rust.
- yarr.fyi is great and I've reached the exciting section, Memory.

#### Day 3 - Wednesday, Jan 17th: Sisyphus stuck in integer overflow

- Attended Creative Coding. The prompt was "With great power...". I created a game to demonstrate integer overflow, which can occur when using a higher power (exponent). After much pondering, I decided to base the game on Sisyphus. In it, Sisyphus pushes the boulder up a mountain but never reaches the top due to integer overflow, thus remaining stuck in a loop. [Here's](https://playcode.io/1729085) the codepen.

    ![](/sisyphus-overflow.gif)


- Easily wasted an hour or two trying to figure out a weird Zoom issue. I tried a bunch of things with Liz and nothing worked. I was able to access it on the web but not through the client. Anyway, it started working today so it's all good now.

- Hung out at RC Cafe.
- Non-programming talks were great! Though, they also made me hungry at 4 am (Not great). Pietro gave a talk on his favourite pasta recipes. I loved how detailed he was, he brought all the utensils and equipment on his desk to show us. [Here](https://docs.google.com/presentation/d/1D6eN7J-UlPvsJttPWKrdqxDCVfKMAdH-2Iu0KJ5hGBA/edit#slide=id.p) are the slides for it. Jen Hsin gave an impromptu talk on instant noodles.

#### Day 4 - Thursday, Jan 18th: Presentations!

- Impossible day - In the meeting I said I would like to make a distributed KV store. I did research a bit on it and then decided not to do so. I just found a bit of momentum with Crafting Interpreters and learning Rust, and I didn't want to distract myself with anything new. Perhaps I'll do something on the next Impossible day.

- Attended the Crafting Interpreters study group. I went very unprepared, I'm yet to finish the 3rd chapter, but it was super informative to attend regardless. I've decided to do the first part in Java. I plan to quickly take speed and at least finish Chapter 5 by the next meeting.

- Pair programmed (kind of) with Erika Rowland. She wanted to document her TUI framework written in Gleam. We mostly spent checking out the codebase, demos, and debugging a weird bug related to line clear on re-render. It was nice to check out Gleam. She was kind enough to explain all the things that seemed weird to me. Like, it doesn't have if statements?? Gleam only has `case` and a `use` statement for control flows. I also got to know some cool Go libraries for TUI. [Bubbletea](https://github.com/charmbracelet/bubbletea) and [Lipgloss](https://github.com/charmbracelet/lipgloss).

- Chapter 3 Crafting Interpreters reading.

- Weekly presentations and impossible day demos.

#### Day 5 - Friday, Jan 19th:

- Finished reading Chapter 3 of Crafting Interpreters.

- Had a coffee chat with P.B. We discussed a variety of topics, including old website designs, our experiences so far at RC, comparing our productivity to that of [Julia Evans](https://jvns.ca/blog/2017/09/17/how-i-spent-my-time-at-the-recurse-center/), and being nocturnal.
- Attended the co-op chat event on worker cooperatives, which was super insightful. There were many questions and answers. I asked how salaries and promotions work. The answer was no promotions and salaries get split equally. It only left me with more questions!

- Slept early because I had to attend a local Python meetup. Not because I've deep interests in Python, but because I left my water bottle there during the last Elixir meetup.
I'm yet to blog about my weekly reflections but my weekend was super tight this time.

## Reflections

End of 3 weeks!! Or maybe not. Since our batch kicked off midweek, it's more like 2.5 weeks, isn't it? And honestly, should the first week even count? That brings us down to 1.5 weeks. Let's round it off for simplicity's sake: it's been a week. Yes, just a week has passed, and I'm thoroughly enjoying my time here.

My pace is slow, and I'm still a lot distracted. Winters just elevate laziness.