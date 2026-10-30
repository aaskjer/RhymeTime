# Import
<p align="center"><img alt="grafik" src="https://github.com/user-attachments/assets/2c17f5a0-15f3-4396-a277-a66638017fb3"> </p>

Click `Import` in [streamer.bot](https://streamer.bot/) and drag the [RhymeTime.sb](https://github.com/aaskjer/RhymeTime/releases) file into the window, or paste the [import string](https://github.com/aaskjer/RhymeTime/blob/main/Import-String.md).

<p align="center"><img alt="grafik" src="https://github.com/user-attachments/assets/d3d8ecfd-018d-4052-9056-c72438d5c613"></p>

Click `Import`, then `Yes` on both popups that follow.

## Enable Commands
<p align="center"><img alt="grafik" src="https://github.com/user-attachments/assets/004c325b-8673-430d-91b9-72c9a8931663"></p>

Both commands ship disabled. Enable `!Rhyme` and `!RhymeBattle` in the `Commands` tab, or nothing
answers in chat. `!RhymeBattle` is restricted to the `Moderators` group on the command itself —
change that there if you want someone else to be able to open a battle.

# Setup
<p align="center"><img alt="grafik" src="https://github.com/user-attachments/assets/8452f85a-daf0-4574-a28c-e9fd0c2eeecf"></p>

Go to `Actions`, select `[RT] - Settings`, right-click the `Test` trigger and choose `Test Trigger`.
That opens the settings window.

Eight pages sit on the rail down the left side. `Ctrl+1` to `Ctrl+8` jump between them, `Ctrl+S`
saves. Every field carries a tooltip, so hovering usually answers the question faster than this page
does.

Twitch, YouTube and Kick all play, always — there is nothing to switch on. Restrict the
Streamer.bot commands if you want the game off a platform.

## Game
<p align="center"><img alt="Game page" src="https://github.com/aaskjer/RhymeTime/blob/main/Assets/setup-guide/game.png?raw=true"></p>

The round and what it costs. How long a chatter has to answer, how many wrong rhymes they may
offer, which word bank a round draws from, and whether a guess that merely ends the right way is
checked against a dictionary first.

Under it the currency — the Streamer.bot user variable the stake comes out of and the name that
fills `{currency}`. Currency Core by StreamUP and LOYALTY POINTS by tawmae are found on their own
and override both fields, Currency Core first, so those two need nothing from you.

Then the bets and the payout. The default bet is what `!Rhyme` stakes without
an amount; the minimum and maximum frame what a chatter may type. Set the default bet to `0` and the
game is **free**: nothing is staked and nothing is paid out, and the header says so.

The payout multipliers are per word bank: a win pays the stake times the multiplier of the bank the
word came from.

The two cooldowns at the bottom are written onto the `!Rhyme` command itself when you save, so
Streamer.bot's own cooldown fields follow this page rather than fighting it.

## Battle
<p align="center"><img alt="Battle page" src="https://github.com/aaskjer/RhymeTime/blob/main/Assets/setup-guide/battle.png?raw=true"></p>

A moderator runs `!RhymeBattle` and the whole chat races for the same word. The first valid rhyme
takes the prize and the battle closes; nobody else pays anything. The answer window is the same
*Seconds to answer* as a normal round, and the word comes from the same banks.

The one setting here is the prize for a battle nobody staked for. `!RhymeBattle 500` stakes 500 of
the moderator's own instead, and then the winner takes that — if nobody rhymes in time it goes back.
The minimum and maximum bet from the Game page apply to a staked battle as well.

## Word banks
<p align="center"><img alt="Word banks page" src="https://github.com/aaskjer/RhymeTime/blob/main/Assets/setup-guide/word-banks.png?raw=true"></p>

One target per row with its rhymes beside it, separated by commas. The picker at the top chooses
which of the three banks you are editing; all three are saved together.

The rhymes you list are examples, not the whole answer: what they have in common at the end is what
the round accepts. Three rhymes ending in `AT` accept any dictionary word ending in `AT`. One lonely
rhyme has nothing to agree with, so half of it is used — list two or three and the round behaves
predictably.

A target **with spaces in it** is a line to finish instead of a word to rhyme. Then the whole reply
has to match one of the answers you listed, so write them out in full.

A row only reaches the game once it has a target and at least one rhyme; the pill above the table
counts the usable ones. *Restore this bank* puts the shipped words back into the bank you are
looking at and leaves the other two alone. Nothing is written until you save.

## Access
<p align="center"><img alt="Access page" src="https://github.com/aaskjer/RhymeTime/blob/main/Assets/setup-guide/access.png?raw=true"></p>

Who may not play. Names on the blocked list are ignored when they run the command, with no reply in
chat; so is everyone in a blocked Streamer.bot group (`Settings` → `Groups`). A group that does not
exist is skipped and logged rather than failing the round.

Permissions themselves belong to the commands in Streamer.bot's `Commands` tab — this page only
takes people out of the game.

## Messages
<p align="center"><img alt="Messages page" src="https://github.com/aaskjer/RhymeTime/blob/main/Assets/setup-guide/messages.png?raw=true"></p>

Every line the game says in chat behind one picker, grouped into Round, Battle, Bets and Cooldown.
Pick one and you get its editor, the placeholders it accepts as clickable chips, and a preview of
the finished line.

The four bet reasons fill `{reason}` inside *Bet refused*, so that one line is the frame around all
of them. Emptying *Examples after a loss* posts nothing after a lost round.

The number format and which account speaks sit at the bottom — the bot account and `/me` apply
separately to the game's messages and to the cooldown replies. `/me` is Twitch only.

## Overlay
<p align="center"><img alt="Overlay page" src="https://github.com/aaskjer/RhymeTime/blob/main/Assets/setup-guide/overlay.png?raw=true"></p>

A browser source for OBS that shows the round on stream: the word with the ending picked out, the
clock, the attempts left, and then the rhyme that won it and what it paid. It ships inside the
import, so there is nothing to download.

Switch *Send rounds to the overlay* on, then switch Streamer.bot's own WebSocket server on under
`Servers/Clients` → `WebSocket Server` and tick *Auto Start*. The port on this page has to be the one
shown there, 8080 unless you changed it. If you turned its authentication on, add `&password=`
followed by that password to the end of the URL.

### Set it up in OBS

**Set the overlay up in OBS** does the rest for you: it saves, writes the overlay page, and over
Streamer.bot's OBS connection creates the scene and puts a browser source in it, the size of your
canvas, pointed at the overlay. OBS has to be connected in Streamer.bot under
`Stream Apps` ▸ `OBS Studio`. *Connection #* is 0 unless you have more than one OBS there; *Scene*
is created if it is not there yet, and a *Source* name OBS already knows is left alone rather than
overwritten.

By hand works too: *Copy URL* writes the page to `Chat Games/RhymeTime/Overlay` and copies its
address — saving with the overlay on writes it as well — then add a **Browser** source in OBS,
untick *Local file*, paste the URL and set the size to 1920 × 1080. *Try the demo* opens the same
page in your browser playing sample rounds, which is the easiest way to place and size the source
before anyone plays.

### How it looks

Everything under *Size and place*, *What it shows* and *Colours* travels with the round itself, so a
change is on screen the next time somebody plays and OBS never has to be touched again.

*Place* puts the card left, centre or right; *Size %* scales it; *Result shown* is how long the
winning rhyme, or the rhymes after a lost round, stays up. The four switches take the ending pill,
the attempt dots, the stake chip and the rhymes after a loss off the card. *Accent* colours the
word's ending, the wordmark and the clock bar, with every lighter shade worked out from it;
*Battle*, *Won* and *Card* do the same for a battle, a win and the card behind it all. Click a
swatch for the picker.

The card follows one round at a time, the newest: a battle takes the card from a single-player round
that is still running.

What this page does not reach goes in the Browser source's own *Custom CSS*, which is read after
these settings and wins:

```css
:root { --rt-width: 480px; --rt-edge: 40px; --rt-radius: 8px; }
```

The URL takes `&platform=twitch` to show one platform's rounds only, `&lang=de` for the German
wording, `&position=center` to overrule *Place*, and `&debug=1` to see whether it reached
Streamer.bot.

## How to play
<p align="center"><img alt="How to play page" src="https://github.com/aaskjer/RhymeTime/blob/main/Assets/setup-guide/how-to-play.png?raw=true"></p>

The rules in short, and where the two files live:

```
Chat Games/RhymeTime/RT-settings.json    ← everything on these pages, every chat line
Chat Games/RhymeTime/RT-wordbank.json    ← the three word banks
```

Both sit under your Streamer.bot folder. Editing them by hand is never necessary — the settings
window writes all of it, keeps the previous copy as `.bak`, and sets a damaged file aside as
`.broken` rather than overwriting it.

## About
<p align="center"><img alt="About page" src="https://github.com/aaskjer/RhymeTime/blob/main/Assets/setup-guide/about.png?raw=true"></p>

The version, the links to the repository and the releases, and what the buttons along the bottom do.
Opening the window also asks GitHub for the latest release in the background; if there is a newer
one, a pill appears in the header.

---

[Frequently Asked Questions](https://github.com/aaskjer/RhymeTime/blob/main/FAQ.md)
