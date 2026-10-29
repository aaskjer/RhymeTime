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
  <a href="Setup-Guide.md"><b>Setup Guide</b></a> &nbsp;·&nbsp;
  <a href="FAQ.md"><b>FAQ</b></a> &nbsp;·&nbsp;
  <a href="Import-String.md"><b>Import String</b></a> &nbsp;·&nbsp;
  <a href="https://github.com/aaskjer/RhymeTime/releases"><b>Download</b></a>
</p>

---

## A round in chat

This is the shape of a round as it ships — placeholders and all. All 19 chat lines are yours to
rewrite on the Messages page.

```
!Rhyme 250
→ Nova, find a rhyme for: DREAM! You have 30 seconds. Bet: 250 Points

i think... BEAM
→ Nova rhymed 'DREAM' with 'BEAM'! +500 Points [Total: 3.250 Points]
```

A wrong guess costs an attempt, not the round. Run out of attempts or out of time and the stake is
gone, with up to five of the rhymes you listed posted after it.

```
!RhymeBattle
→ ⚔️ BATTLE TIME! First to rhyme with 'LIGHT' wins 500 Points! You have 30s!
→ 🏆 Kira won the battle by rhyming 'LIGHT' with 'FLIGHT'! +500 Points (Total: 1.900 Points)
```

---

## How it works

| Event | Trigger | Result |
|---|---|---|
| 🎮 **Round starts** | A chatter runs `!Rhyme` | A word is drawn from the chosen bank, the stake is named and the clock starts. |
| ✅ **Rhyme found** | The guess rhymes | The round is won and the stake pays out at the bank's multiplier. |
| ❌ **Wrong guess** | The guess looks like an attempt but misses | One attempt is used up. Anything that does not look like an attempt is ignored entirely. |
| 🚫 **Out of attempts** | The attempt limit is reached | The round is lost and the stake is gone. |
| ⏰ **Out of time** | The clock runs out | Same, plus examples of what would have worked. |
| ✍️ **Line to finish** | The target has spaces in it | The whole reply has to match one of the answers you listed, punctuation ignored. |
| ⚔️ **Battle** | A moderator runs `!RhymeBattle` | One word for the whole chat. The first valid rhyme takes the prize; nobody else pays anything. |
| ↩️ **Battle expires** | Nobody rhymed in time | Any stake the moderator put up goes straight back. |

Each chatter plays their own round, and each platform can have one battle running at a time.

---

## What it does

- **Rhymes it was never told about still count.** The words you list are the examples; what they
  have in common at the end is what the round accepts. `BAT, HAT, MAT` accepts anything ending in
  `AT` — checked against a dictionary first, so `FLAT` wins and `XQAT` does not.
- **Lines to finish, not just words.** A target with spaces in it turns the round into a line to
  complete: *ROSES ARE RED VIOLETS ARE BLUE …* expects the whole answer.
- **Answers in ordinary chat.** No second command — only the last word of the message is read, so
  "hmm maybe DREAM" works. In a line round the whole message counts.
- **Three word banks.** Easy, medium and hard, each with its own payout multiplier, editable in the
  settings window. A round draws from the one you pick, or randomly from whichever have words.
- **Bets or free play.** Chatters stake a number, or `all`, `half`, `third`, `quarter`, `random`,
  within the minimum and maximum you set. Put the default bet at `0` and the whole game is free —
  nothing staked, nothing paid.
- **Battles for the whole chat.** A moderator opens one word to everyone, with a fixed prize or
  their own stake on the line.
- **Every line is yours.** 19 chat messages in one place, with a live preview and clickable
  placeholders.
- **One settings window.** Seven pages, `Ctrl+1`…`Ctrl+7`, `Ctrl+S` to save, light and dark.

---

## Commands

These are the default names — in Streamer.bot you can bind them to whatever you like. Both commands
ship **disabled**; enable them in the `Commands` tab after importing.

| Command | Who | What it does |
|---|---|---|
| `!Rhyme` | Everyone | Starts a round at the default bet |
| `!Rhyme 250` | Everyone | Starts one at 250, within the minimum and maximum |
| `!Rhyme all` | Everyone | Also `half`, `third`, `quarter` and `random` |
| *just type in chat* | Everyone | Your answer |
| `!RhymeBattle` | Moderators | Opens a battle for the whole chat, paying the battle reward |
| `!RhymeBattle 500` | Moderators | Opens one and stakes 500 of their own — the winner takes the stake |

Permissions and cooldowns belong to the commands themselves. The two cooldowns on the Game page are
written onto `!Rhyme` whenever you save, so Streamer.bot's own fields follow the settings window.

---

## How a guess is judged

For a word round, in this order:

1. The guess **is the target word** → never counts.
2. The guess **is one of the rhymes you listed** → always counts, dictionary or not.
3. The guess **ends the way the listed rhymes end** → counts if the dictionary agrees it is a word.

The accepted endings are worked out from the rhymes you listed: the longest ending enough of them
share, at least two letters. A single listed rhyme has nothing to agree with, so half of it is used.
The dictionary check asks [wordotron.com](https://wordotron.com) once per word and caches the
answer. It fails open — if the lookup is slow or unreachable the guess is accepted, so an outage
never rejects a correct rhyme. Switch it off and anything with the right ending wins.

A line to finish skips all of that: the reply has to match one of the answers you listed, with
punctuation and double spaces ignored.

---

## Points

The currency is detected from StreamUP's **Currency Core** when it is installed — the game reads its
`currency_ProductSettings` global and uses the variable and name from there. Any other currency
takes one variable name on the Game page.

A win pays `stake × multiplier` for the bank the word came from (1.5× easy, 2× medium, 3× hard by
default). A loss costs the stake. A battle pays the moderator's stake if they staked one, otherwise
the flat battle reward.

---

## Credits & links

[aaskjer on Twitch](https://twitch.tv/aaskjer) · [aaskjer.github.io](https://aaskjer.github.io/) ·
[Streamer.bot](https://streamer.bot) · [nate1280](https://www.patreon.com/c/nate1280/home) ·
[wordotron.com](https://wordotron.com) (dictionary check) ·
[StreamUP Currency Core](https://streamup.tips/product/currency-core)

Neither project above is affiliated with or endorses RhymeTime.

YOU ♡
