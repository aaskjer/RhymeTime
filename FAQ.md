# ❓ RhymeTime — FAQ

---

## 🛠️ Setup & Configuration

**Q: Where are the files stored?**

Under your Streamer.bot base directory:

```
Chat Games/RhymeTime/RT-settings.json    ← settings and every chat message
Chat Games/RhymeTime/RT-wordbank.json    ← the three word banks
```

Editing either by hand is never necessary — the settings window writes both.

***

**Q: Nothing happens when I type `!Rhyme`.**

The commands ship disabled. Open Streamer.bot's `Commands` tab and enable `!Rhyme` and
`!RhymeBattle`. If they are enabled and still silent, check that the `RhymeTime Game` and
`RhymeTime Battle` actions are enabled too, and that the chosen word bank has words in it.

***

**Q: How do I open the settings window?**

`Actions` → `[RT] - Settings` → right-click the `Test` trigger → `Test Trigger`. Only one window
opens; triggering it again brings the one you have to the front.

***

**Q: The settings file is damaged. Did I lose everything?**

No. Every save keeps the copy it replaced as `RT-settings.json.bak`. If the file cannot be parsed,
the window sets it aside as `RT-settings.json.broken`, loads the `.bak`, and tells you which of the
two happened. The game itself falls back to the defaults for that round rather than failing, so a
damaged file never leaves chat without an answer.

***

**Q: How do I reset the settings?**

The circular arrow at the bottom left resets every page, the half arrow only the page in front of
you. Both ask first. Neither touches the word banks — those have *Restore this bank* on their own
page, per bank.

***

**Q: I saved but the game still behaves the old way.**

It should not: the game reads the settings fresh on every command, so the next round already runs on
the new values. Nothing needs restarting. The two cooldowns are the exception worth knowing about —
they are written onto the `!Rhyme` command when you save, which is where Streamer.bot reads them.

---

## 🎮 Starting & Ending a Round

**Q: Who may start a round?**

Anyone, unless you say otherwise. Permissions live on the command in Streamer.bot's `Commands` tab —
set a group there and only that group can run `!Rhyme`. `!RhymeBattle` ships restricted to the
`Moderators` group the same way.

***

**Q: Can two people play at once?**

Yes. Every chatter has their own round, with their own word, clock and attempts. Running `!Rhyme`
while your own round is still open gets you *you already have an active round!* and nothing else.

Battles are the opposite: one per platform at a time, for everyone.

***

**Q: How do I stop a round?**

There is no kill command — a round ends when the clock runs out, when the attempts are used up, or
when it is won. Rounds live in memory only, so restarting Streamer.bot clears whatever was running.

***

**Q: Does the game reply when the command is on cooldown?**

Yes, with the two Cooldown messages, and the stake is not taken. Set either cooldown to `0` to turn
it off.

---

## 💬 Commands & Answering

**Q: What are the in-chat commands?**

| Command | Who | What it does |
|---|---|---|
| `!Rhyme` | Everyone | Starts a round at the default bet |
| `!Rhyme 250` | Everyone | Starts one at 250, within the minimum and maximum |
| `!Rhyme all` · `half` · `third` · `quarter` · `random` | Everyone | Stakes a share of what they have |
| *just type in chat* | Everyone | Your answer |
| `!RhymeBattle` | Moderators | Opens a battle paying the battle reward |
| `!RhymeBattle 500` | Moderators | Opens one and stakes 500 of their own |

These are the names as they come in the import; rename them in Streamer.bot's `Commands` tab if you
like. The scripts follow the command, not its name.

***

**Q: How do chatters answer?**

In ordinary chat, no command. Only the **last word** of the message is read, so "hmm maybe DREAM"
answers `DREAM`. A line to finish reads the **whole** message instead, with punctuation and double
spaces ignored.

***

**Q: Does every wrong guess cost an attempt?**

No — only guesses that look like an attempt. A guess counts as an attempt when it at least ends with
the same two letters as one of the accepted endings; anything else in chat is ignored, so normal
conversation does not burn through a round. The attempt limit is on the Game page.

***

**Q: Does the target word itself count as a rhyme?**

No. `DREAM` for `DREAM` is rejected, and it costs an attempt like any other miss.

---

## 🎯 Rhyme Matching

**Q: How does the game decide whether something rhymes?**

In this order:

1. The guess **is the target word** → never counts.
2. The guess **is one of the rhymes you listed** → always counts, dictionary or not.
3. The guess **ends the way the listed rhymes end** → counts if the dictionary agrees it is a word.

***

**Q: Where do the accepted endings come from?**

From the rhymes you listed. The game takes the longest ending enough of them share — at least two
letters — so `BAT, HAT, MAT, FLAT` accepts anything ending in `AT`. A single listed rhyme has
nothing to agree with, so half of it is used: `DOVE` alone accepts anything ending in `VE`.

List two or three rhymes per word and the round behaves predictably. List one and it gets generous.

***

**Q: What is the dictionary check?**

*Check guesses against a dictionary* on the Game page. A guess that merely ends the right way is
looked up at [wordotron.com](https://wordotron.com) before it counts, so `FLAT` wins and `XQAT` does
not. Each word is asked once and the answer is remembered for the session.

It **fails open**: if the lookup is slow or unreachable, the guess is accepted. A dictionary outage
can let a nonsense word through, but it will never reject a correct rhyme. Switch the check off and
anything with the right ending wins.

***

**Q: What is a line to finish?**

A target with spaces in it. *ROSES ARE RED VIOLETS ARE BLUE …* is not a word to rhyme but a line to
complete, and the rhymes you list for it are the full answers. The chatter's whole message has to
match one of them; endings and the dictionary play no part.

---

## 💰 Points, Bets & Payout

**Q: What currency does the game use?**

StreamUP's **Currency Core** is picked up automatically — the game reads its
`currency_ProductSettings` global and takes the variable and the display name from there. Without
it, the *Points variable* and *Points name* on the Game page apply: the variable is the Streamer.bot
user variable the stake comes out of, the name fills `{currency}` in chat.

***

**Q: How is a win calculated?**

```
payout = stake × the multiplier of the bank the word came from
```

Defaults are 1.5× easy, 2× medium and 3× hard, all on the Game page. A lost round costs the stake.

***

**Q: Can I run the game without points?**

Yes. Put the **default bet** at `0` and the game is free: nothing is staked, nothing is paid out,
and an amount typed after the command is ignored. The window shows a *Free game on* pill while that
is the case, so a message about points means what it says.

***

**Q: What can a chatter type as a bet?**

A number, or `all`, `half`, `third`, `quarter`, `random` — each a share of what they actually have.
A bet below the minimum, above the maximum, above their balance, or not a number at all is refused
with the matching reason and no round starts. Set the minimum or maximum to `0` to turn that limit
off.

***

**Q: When is the stake taken?**

On a loss, not at the start. A won round adds the payout, a lost one subtracts the stake, and a
round that never starts — refused bet, cooldown, blocked user — costs nothing.

---

## ⚔️ Battles

**Q: What is a battle?**

One word for the whole chat. A moderator runs `!RhymeBattle`, everyone answers in chat, and the
first valid rhyme takes the prize and closes the battle. Nobody but the moderator stakes anything,
and losing costs nothing.

***

**Q: What does a battle pay?**

The **battle reward** on the Battle page (500 by default). `!RhymeBattle 500` instead stakes 500 of
the moderator's own points, and the winner takes that — the minimum and maximum bet from the Game
page apply to it. A battle nobody wins hands a staked amount straight back to the moderator who put
it up.

With the default bet above `0`, a bare `!RhymeBattle` stakes the default bet rather than paying the
reward.

***

**Q: Can two battles run at once?**

One per platform. Twitch, YouTube and Kick each have their own, so a battle on Twitch does not block
one on YouTube. A second `!RhymeBattle` on the same platform gets *a battle is already in progress*.

***

**Q: How long is the answer window?**

The same *Seconds to answer* as a normal round, and the word comes from the same banks and
difficulty.

---

## 📚 Word Banks

**Q: Where do the words come from?**

`RT-wordbank.json`, edited on the **Word banks** page. Three banks — easy, medium and hard — each a
list of targets with their rhymes beside them, separated by commas. The picker chooses which bank
you are editing; all three save together.

***

**Q: How many rhymes should I list?**

Two or three. They are examples the game learns the accepted ending from, not the whole answer, so
one rhyme on its own makes the round generous and five near-identical ones make it strict.

***

**Q: A row is in the bank but never comes up.**

A row only reaches the game once it has a target **and** at least one rhyme. The pill above the
table counts the usable rows, so compare it with what you see.

***

**Q: Which bank does a round draw from?**

*Difficulty* on the Game page. `Random` picks one of the three that actually has usable words in it.
If the chosen bank is empty the round does not start and chat gets the *Empty word bank* message.

***

**Q: Can I get the shipped words back?**

*Restore this bank* on the Word banks page, per bank — the other two are left alone, and nothing is
written until you save. Resetting the settings does not touch the word banks.

---

## 👥 Access & Cooldowns

**Q: How do I keep someone out of the game?**

The **Access** page. A name on the blocked list is ignored when they run the command, with no reply
in chat, and so is everyone in a blocked Streamer.bot group (`Settings` → `Groups`). A group that
does not exist is skipped and logged rather than failing the round.

***

**Q: Why are permissions not in the settings window?**

Because Streamer.bot already has them, per command, with groups and users. Everything the game does
hangs off `!Rhyme` and `!RhymeBattle`, so restricting those is the one place that cannot be
contradicted.

***

**Q: Which cooldown applies to what?**

Both sit on the Game page and both belong to `!Rhyme`: one for the whole chat, one per chatter. The
window writes them onto the command when you save. `!RhymeBattle` keeps its own cooldowns in
Streamer.bot.

---

## 💬 Messages

**Q: Can I change what the game says?**

All 19 lines, on the **Messages** page, grouped into Round, Battle, Bets and Cooldown. The preview
under the box shows how the line will read in chat, and the chips insert the placeholders that line
accepts. A placeholder a message does not accept is left as text.

***

**Q: What are the four Bets reasons for?**

*Bet refused* is the frame; the four reasons fill its `{reason}` depending on what was wrong —
not a number, cannot afford it, under the minimum, over the maximum. Rewriting the frame keeps all
four.

***

**Q: How do I stop the examples after a lost round?**

Empty *Examples after a loss*. An empty message posts nothing.

***

**Q: Why does `/me` do nothing on YouTube and Kick?**

They have no `/me`. The toggle is Twitch only, as the pill beside it says; elsewhere the message
goes out as plain chat. The bot account and `/me` apply separately to the game's messages and to the
cooldown replies.

---

## 🌐 Multi-Platform

**Q: Which platforms play?**

Twitch, YouTube and Kick, always. There is no platform selection — if you want the game off a
platform, restrict the commands in Streamer.bot.

***

**Q: Are points shared between platforms?**

No. Points are Streamer.bot user variables, and those are per platform. A viewer on Twitch and the
same person on YouTube are two players with two balances.

***

**Q: Does the answer go back to the right chat?**

Yes. The platform is read from the event, and the reply goes to the chat the command came from.

---

## 🔔 Update Notifications

**Q: How do I know when there is a new version?**

Opening the settings window asks GitHub for the latest release in the background. If there is a
newer one, a pill appears in the header and a click opens the releases page. The check never holds
the window shut — if GitHub is slow or unreachable, the pill simply does not appear.

***

**Q: Does updating lose my settings?**

No. `RT-settings.json` and `RT-wordbank.json` are yours and stay where they are; the import replaces
the actions, not the files. A setting a new version adds arrives at its default.

---

# Is RhymeTime an AI Slop?

Partially, yes. This script grew out of input from the Streamer.bot community with AI along for the ride.
But i put a lot of heart and time into it, with the goal of building a chat game that is robust, fair and easy to use for everyone.
I understand that people, especially IT savvy people, will dislike the project because of the use of AI, and i absolutely understand and support their point of view.
Still, i had a lot of fun making it, as with all my other projects — i used it to "learn" coding and put AI to something worthwhile.

AI can create bugs, and i am not a developer in classical terms. But i spend a reasonable amount of time fixing any bug that turns up while testing.
If you still find bugs or have something to say, please let me hear it :)
