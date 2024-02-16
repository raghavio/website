---
title: "Week 1 Of Recurse Center"
date: 2024-01-07T12:38:52+05:30
draft: false
---

## A start full of excitement

Greetings! My name is Raghav, and I'm attending the Winter 2 batch of Recurse Center remotely from New Delhi, India. I've just completed my first week at the Recurse Center. The week has been a whirlwind of activities and emotions, quite overwhelming at times. Meeting new people, figuring out timezones, discovering topics I didn't know existed, and second-guessing my RC plans were just a few of the challenges. Due to the holidays, our batch began on a Wednesday, making the first week just three days long.

Here's a rundown of my day to day experience and reflections so far.

#### Day 1 - Wednesday, Jan 3rd: Welcoming and Introductions
The first day commenced with welcome calls and introductions. This was at 9:30PM IST. The RC faculty and the current batch got together in a Zoom call. This included not only my batch, Winter 2, but also the preceding batch, Winter 1. At Recurse, a new batch starts every six weeks, ensuring an overlap between two batches at all times.

In the Zoom call, we were introduced to the RC faculty. They briefed us on RC's philosophy, the [self directives](https://www.recurse.com/self-directives), and how to be a dramatically better programmer.

Liz welcomed us with this beautiful note:
> - you’ve been programming for 3 months or 10 years
>- can't wait to get started, or if you have no idea where to begin
> - you consider yourself an Introvert, an extrovert, or anywhere in between
> - whether you’re joining us during the middle of the day or the middle of the night
> - if you use Windows, Linux, macOS, BSD, or something else
> - if you are object oriented, functional, imperative, declarative, multi paradigm, or not sure what any of those things mean
> - if you want to write apps, servers, languages, visualizations, games, or art
> - if you find beauty in the highest levels of abstraction, the lowest levels of the machine, the process of building things, or the end result.

For the meet and greets, Nick arranged us in several Zoom breakout rooms, where we got to meet randomly selected people in our batch for a few minutes. I believe I met around 12 to 15 folks. This was super fun and I had some great conversations. By the end, I was low-key exhausted from repeatedly introducing myself.

Following this, we were encouraged to share our excitement and nervousness, which were then compiled into a list. The point was to make ourself feel welcome and that we are not alone with these thoughts.

The Zoom call ended with a short skit explaining the [social rules](https://www.recurse.com/social-rules) of RC. In this skit, a faculty member would deliberately violate a social rule, and we had to intervene and point it out.

After the Zoom call, I spent some time figuring out Zulip, open source Slack alternative and, [Virtual RC](https://www.recurse.com/virtual-rc), a Club Penguin style interactive map of the offline space in Brooklyn. All these new experiences were quite overwhelming.

After going through all the new introductions on Zulip and subscribing to the streams (channels) I was interested in, I decided to call it a day.

#### Day 2 - Thursday, Jan 4th: Pairing workshop and website planning

During the day, I was mostly procrastinating on setting up a website (this thing). The first set of events for day 2 was the pairing workshop. But before that, I had a quick coffee chat with Emily Bernier. No, none of us were having coffee or any other beverage. It was also 10 pm for me. These are simply termed 'coffee chats'. These are scheduled by a bot for a one-on-one Zoom chat with a random recurser. 

The pairing workshop started with Liz explaining how pairing is the essence of making the most out of your time at RC. Followed by a short Zoom recording of two folks pairing on a Tic Tac Toe game in Ruby. That recording was so fun and completely unlike any pairing I've done at work, which is mostly sad and depressing.

Prior to the workshop, we were asked to fill out an Excel sheet, listing the programming languages we are comfortable with for pairing.

We were going to create [Mastermind](https://en.wikipedia.org/wiki/Mastermind_(board_game)). It's similar to Wordle and uses colors instead of words. Donald Knuth has also written a [paper](https://www.cs.uni.edu/~wallingf/teaching/cs3530/resources/knuth-mastermind.pdf) on how to play it optimally.

I was matched with Felix in one of the Zoom breakout room, who also had Clojure as his preferred language of choice for the workshop. It was super fun to pair with him and we managed to get a working implementation of the game in an hour or so. Here's a code for it:
```Clojure
(require '[clojure.string :as str])
(def colors ["red" "blue" "yellow" "green" "purple" "pink"])

(defn secret
  [colors]
  (mapv (fn [_] (rand-nth colors)) (range 4)))

(defn match
  [secret color-input index]
  (cond
    (= (get secret index) color-input) :green
    (some (fn [color] (= color color-input)) secret) :white
    :else :black))

(defn check-guess
  [secret guess]
  (map-indexed (fn [index color-input] (match secret color-input index)) guess))

(defn parse-input
  [line]
  (str/split line #" "))

(def winning-result
  [:green :green :green :green])

(defn run-game
  [secret]
  (loop [attempts 1]
    (let [result (check-guess secret (parse-input (read-line)))
          game-over? (or (= attempts 10) (= result winning-result))]
      (println "Attempt: " attempts "Result: " result)
      (when-not game-over?
        (recur (inc attempts))))))

(let [secret (secret colors)]
  (println "Secret: " secret)
  (run-game secret))
```

After the workshop, I started looking for a Static Site Generator (SSG) for my website. A lot of folks recommended Hugo so I decided to go with that. For the website, I have an ambitious project of building one from scratch. I want it to be old school, something that truly represents my style. The clothes I wear, prints I own, decor I have, music I listen to, pictures I've clicked. I'm not sure how to depict those in CSS yet but I do look at [People Tree](https://www.peopletreeonline.com/home.html)'s website for inspiration. They have perfectly captured the kind of personalization I would love to see in my website.

The day ended with a chill audio chat with Reed Spool and Vedashree Divekar in the Cafe area of the Virtual RC. We discussed websites, animations, JSX on server side, backpacking. I found out about the GSAP animation library and their [website](https://gsap.com/) is wicked.

#### Day 3 - Friday, Jan 5th: Setting up the Website

Mostly a chill day but managed to get some work done during the night. After contemplating for an hour, I finalized on the domain name. It was quick to setup a blog on Hugo. I wrote a [short post](/posts/recurse-center/) about the Recurse Center and outlined my plans.

Via Zulip, I found out about [Cloudflare Pages](https://pages.cloudflare.com/) and decided to use it for deployment. It has Github integration and I was up and ready in a jiffy. You can do the same on Github Pages but I'm guessing the performance of Cloudflare will be better since it uses their edge network.

### Reflections

I find myself scattered, trying to absorb the multitude of events, activities, and Zulip streams. Everyone is incredibly smart, working on things I've never even heard of. I was told all these feelings are normal and it takes two to three weeks to really settle and focus.

I'm beginning to reconsider my initial plan. I've come across some interesting study groups that I would rather pursue. Mainly the Crafting Interpreters and one Rust related.