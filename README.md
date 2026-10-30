<h1 align="center">RhymeTime</h1>

<p align="center">
  <b>Rhyme battles straight in your chat — on Twitch, YouTube and Kick.</b><br>
  One chatter against the clock, or the whole chat racing for the same word.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/platforms-Twitch%20%7C%20YouTube%20%7C%20Kick-9146FF" alt="Platforms">
  <img src="https://img.shields.io/badge/tool-streamer.bot-0b73ff" alt="Streamer.bot">
  <img src="https://img.shields.io/github/license/aaskjer/RhymeTime" alt="License">
  <img src="https://img.shields.io/github/v/release/aaskjer/RhymeTime" alt="Release">
  <img src="https://img.shields.io/github/downloads/aaskjer/RhymeTime/total" alt="Downloads">
</p>

<p align="center">
  <a href="https://github.com/aaskjer/RhymeTime/releases"><b>Download</b></a> &nbsp;·&nbsp;
  <a href="Setup-Guide.md"><b>Setup Guide</b></a> &nbsp;·&nbsp;
  <a href="FAQ.md"><b>FAQ</b></a> &nbsp;·&nbsp;
  <a href="Import-String.md"><b>Import String</b></a>
</p>

---

## 📖 Overview

RhymeTime is a chat game for Streamer.bot. A chatter starts a round with `!Rhyme`, gets a word and answers
in ordinary chat before the clock runs out. A wrong guess costs an attempt, not the round. Moderators can
open a battle with `!RhymeBattle`: one word for the whole chat, and the first valid rhyme takes the prize.

```
!Rhyme 250
→ Nova, find a rhyme for: DREAM! You have 30 seconds. Bet: 250 Points

i think... BEAM
→ Nova rhymed 'DREAM' with 'BEAM'! +500 Points [Total: 3.250 Points]
```

## ✨ Highlights

- 🎤 **Rhymes it was never told about.** The rhymes you list are examples; the ending they share decides what
  counts. `BAT, HAT, MAT` accepts anything ending in `AT`, checked against a dictionary first, so `FLAT`
  wins and `XQAT` does not.
- 📖 **A dictionary that never blocks a correct answer.** The check asks wordotron.com once per word and caches
  the result. If the lookup is slow or unreachable, the guess is accepted.
- ✍️ **Lines to finish.** A target with spaces in it turns the round into a line to complete, such as
  *ROSES ARE RED VIOLETS ARE BLUE …*, and the reply has to match one of your answers.
- 💬 **No answer command.** Only the last word of a message is read, so "hmm maybe DREAM" works. Messages that
  don't look like an attempt are ignored.
- 📚 **Three word banks.** Easy, medium and hard, each with its own payout multiplier: 1.5×, 2× and 3× by
  default.
- 💰 **Bets or free play.** Chatters stake a number or `all`, `half`, `third`, `quarter`, `random`. A default
  bet of `0` makes the whole game free.
- 📺 **An overlay for OBS.** The word on stream with its countdown and the attempts left, then the winning
  rhyme and what it paid. It ships with the import, runs on Streamer.bot's own WebSocket server, and one
  button sets it up in OBS. Place, size, colours and what it shows are all in the window.
- ⚙️ **One settings window.** Eight pages with keyboard shortcuts, light and dark themes, and all 19 chat
  messages with a live preview.

---

## Credits

- **Author:** [aaskjer on Twitch](https://twitch.tv/aaskjer) · [aaskjer.github.io](https://aaskjer.github.io/)
- **Built for:** [Streamer.bot](https://streamer.bot) by [nate1280](https://www.patreon.com/c/nate1280/home)
- **Works with:** [Currency Core by StreamUP](https://streamup.tips/product/currency-core) · [LOYALTY POINTS by tawmae](https://tawmae.xyz/loyalty-points)
- **Data & services:**
  - [wordotron.com](https://wordotron.com): dictionary check
- **Thanks:** YOU ♡

None of the projects above is affiliated with or endorses RhymeTime.
