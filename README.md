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
- 💰 **Bets or free play.** Chatters stake a number or `all`, `half`, `third`, `quarter`, `random`. A Free mode
  switch, or a default bet of `0`, makes the whole game free; `!SetFreeRhyme` and `!EndFreeRhyme` (moderators)
  switch it from chat.
- 🔔 **Hooks for your own actions.** Custom triggers for every won, lost or timed-out round and battle, and for
  Free mode switching, with the round as arguments; `GetLastRoundResult` and `GetLastBattleResult` hand them to
  any action.
- 📺 **An overlay for OBS.** The word on stream with its countdown and the attempts left, then the winning
  rhyme and what it paid. It ships with the import, runs on Streamer.bot's own WebSocket server, and one
  button sets it up in OBS. Place, size, colours and what it shows are all in the window.
- ⚙️ **One settings window.** Eight pages with keyboard shortcuts, light and dark themes, and all 19 chat
  messages with a live preview.

---

## ⚙️ Settings window

The settings action opens a window from [UIFramework for streamer.bot](https://github.com/aaskjer/UIFramework-Streamer.bot),
a separate DLL that is fetched automatically.

- **First open:** a dialog asks whether to download `UIFramework.dll` from the framework's GitHub release into
  `<Streamer.bot>\UIFramework\lib\`. The file is checked against its published SHA-256 before it is used. *No*
  opens that folder so you can put the DLL there yourself; *Cancel* leaves everything as it is.
- **Updates:** when a newer framework release is out, the window asks before it downloads anything. *Cancel* skips
  that version for good.
- **Turning the update check off:** put `"autoUpdate": false` into `uiframework.layout.json`, next to the settings
  file `<Streamer.bot>\Chat Games\RhymeTime\RT-settings.json` (create it as `{ "autoUpdate": false }` if it is not there yet). The window then
  opens with the DLL it has and asks nothing.
- **Without the window:** the game itself never loads the DLL. Disable the settings action and the game plays on
  with its settings file, which you can still edit by hand.

---

## Credits

- **Author:** [aaskjer on Twitch](https://twitch.tv/aaskjer) · [aaskjer.github.io](https://aaskjer.github.io/)
- **Built for:** [Streamer.bot](https://streamer.bot) by [nate1280](https://www.patreon.com/c/nate1280/home)
- **Works with:** [Currency Core by StreamUP](https://streamup.tips/product/currency-core) · [LOYALTY POINTS by tawmae](https://tawmae.xyz/loyalty-points)
- **Data & services:**
  - [wordotron.com](https://wordotron.com): dictionary check
- **Thanks:** YOU ♡

None of the projects above is affiliated with or endorses RhymeTime.
