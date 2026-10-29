# Changelog

Releases are in the [release notes](https://github.com/aaskjer/RhymeTime/releases).
The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [1.0.0] - 2026-10-29

The first release. Three actions — `[RT] - Settings`, `RhymeTime Game` and `RhymeTime Battle` — and
two files of your own under `Chat Games/RhymeTime`.

### Added

- **Single-player rounds.** `!Rhyme` draws a word from one of three banks and gives the chatter a
  clock and a handful of attempts to rhyme with it. Answers go into ordinary chat: only the last
  word of the message is read, so "hmm maybe DREAM" counts. A win pays the stake times the bank's
  multiplier, running out of time or attempts costs it, and up to five of the rhymes you listed are
  posted after a loss.
- **Rhymes the game was never told about.** The rhymes you list are examples: the longest ending
  enough of them share becomes what the round accepts, so `BAT, HAT, MAT` takes any dictionary word
  ending in `AT`. A listed rhyme always counts, the target word itself never does, and a guess that
  does not even end the right way is ignored instead of costing an attempt.
- **A dictionary check** against [wordotron.com](https://wordotron.com) for guesses that merely end
  the right way, one lookup per word and cached for the session. It fails open, so a slow or
  unreachable dictionary never rejects a correct rhyme. Switchable.
- **Lines to finish.** A target with spaces in it is a line to complete rather than a word to rhyme.
  The whole reply is read, punctuation and double spaces ignored, and it has to match one of the
  answers you listed.
- **Battles.** `!RhymeBattle` opens one word to the whole chat and the first valid rhyme takes the
  prize; nobody else pays anything. Moderators only, set on the command. The prize is a flat reward,
  or the moderator's own stake with `!RhymeBattle 500` — which goes back to them if nobody rhymes in
  time. One battle per platform at a time.
- **Bets.** A number, or `all`, `half`, `third`, `quarter` and `random`, framed by a minimum and a
  maximum, with a reason in chat for every refusal. Put the default bet at `0` and the whole game is
  free: nothing staked, nothing paid.
- **Three word banks** in `RT-wordbank.json` — easy, medium and hard, each with its own payout
  multiplier. A round draws from the one you pick, or randomly from whichever have usable words.
- **A settings window** on seven pages: Game, Battle, Word banks, Access, Messages, How to play and
  About. `Ctrl+1`…`Ctrl+7` jump between them, `Ctrl+S` saves, light and dark both included. It
  counts what you have changed, warns about settings that cancel each other out, and resets either
  one page or all of them.
- **A word-bank editor** on its own page: add and remove rows per bank, a count of how many are
  usable, and *Restore this bank* for the words RhymeTime ships.
- **19 chat messages** in one place, grouped into Round, Battle, Bets and Cooldown, each with the
  placeholders it accepts as clickable chips and a live preview of how the line will read in chat.
  The number format, the bot account and `/me` sit beside them, separately for the game and the
  cooldown replies.
- **Twitch, YouTube and Kick**, always, with the reply going back to the chat the command came from.
  There is no platform selection — restrict the commands in Streamer.bot instead.
- **An access page**: blocked viewers and blocked Streamer.bot groups are ignored without a word in
  chat. A group that no longer exists is logged rather than failing the round.
- **Cooldowns written onto the command.** The two cooldowns on the Game page are saved onto `!Rhyme`
  itself, so Streamer.bot's own fields follow the window instead of fighting it.
- **Currency detection.** Currency Core by StreamUP is picked up from its `currency_ProductSettings`
  global, LOYALTY POINTS by tawmae from `tawmae_Settings_LOYALTY POINTS` or the older
  `loyaltyPointsVariable` / `loyaltyPointsName` globals, in that order. Whichever answers first
  supplies both the variable the points live in and the name chat sees; the Game page is only for a
  points system of your own.
- **An update check** in the background when the window opens, as a pill in the header rather than a
  popup that blocks the window.
- Settings and word banks are written atomically: the previous copy is kept as `.bak`, and a damaged
  file is set aside as `.broken` instead of being overwritten. The game falls back to the defaults
  for the round rather than leaving chat without an answer.
