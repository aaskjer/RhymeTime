# Changelog

Releases are in the [release notes](https://github.com/aaskjer/RhymeTime/releases).
The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [2.2.0] - Unreleased

### Added
- **Custom triggers.** Every settled round fires `RT: Round Won`, `RT: Round Lost` or `RT: Round Timeout`, and
  `RT: Round Settled` every time (Custom > Chat Game > RhymeTime), with the round as arguments: `roundOutcome`,
  `roundUser`, `roundUserId`, `roundPlatform`, `roundWord`, `roundGuess`, `roundDifficulty`, `roundBet`,
  `roundAmount`, `roundAttempts`, `roundPreviousPoints`, `roundNewPoints`, `roundCurrency`, `roundFree`. A battle
  fires `RT: Battle Won` or `RT: Battle Timeout` and `RT: Battle Settled`, with `battleOutcome`, `battleWinner`,
  `battleWinnerId`, `battlePlatform`, `battleWord`, `battleGuess`, `battleDifficulty`, `battleStake`,
  `battleReward`, `battleStarter`, `battleStarterId`, `battlePreviousPoints`, `battleNewPoints`,
  `battleCurrency`. `GetLastRoundResult` (RhymeTime Game) and `GetLastBattleResult` (RhymeTime Battle), run
  with an Execute C# Method sub-action, hand the same arguments to any other action.
- **Free mode, and from chat.** A *Free mode* switch on the Game page (a default bet of 0 is free as before);
  `!SetFreeRhyme` turns it on and `!EndFreeRhyme` turns it off (moderators; two new commands in the import,
  disabled until you enable them). The switch is written into the settings file, so the window's pill shows it,
  and chat gets the new Started and Ended messages (Messages page, Free mode). An action of your own can do the
  same with an Execute C# Method on `StartFreeGame` or `EndFreeGame`. `RT: Free Game Start` and
  `RT: Free Game End` fire with it.
- **Show a sample round.** A new button beside *Set the overlay up in OBS* plays one made-up round on every overlay
  that is open, the one in OBS included, in the look saved on the Overlay page, so you can see where the card sits
  without anybody playing. It waits while a real round or battle is on the overlay. *Try the demo* still opens the
  overlay in your browser with sample rounds; the overlay buttons now sit in two rows.
- **An Overlay pill in the window's header** says whether rounds reach the OBS overlay (*Overlay on* / *Overlay
  off*), like the Free game pill.

## [2.1.0] - Unreleased

### Changed
- **The settings action is UIFramework's generic stub.** `[RT] - Settings` carries no layout and no game code any
  more: `RhymeTime Game` declares its window (pages, the `!Rhyme` cooldowns, help and about) beside its settings
  table and answers the window itself (the Overlay page's buttons, the check before saving). Needs UIFramework
  0.9.3 or newer, which the stub fetches; the overlay URL reaches the clipboard through the window.
- **German.** With the window's language set to `de` (the pencil, then *Sprache*), every setting, section, page
  and message of the window reads in German. The help and about pages stay English.

## [2.0.0] - 2026-11-01

The settings window moved into [UIFramework for streamer.bot](https://github.com/aaskjer/UIFramework-Streamer.bot),
one window shared by all of these chat games. The game and the battle play exactly as before; what changed is how
the settings are shown and stored.

### Changed

- **One DLL, downloaded on first open.** `[RT] - Settings` is now a small stub. The first time you open the window
  it asks whether to download `UIFramework.dll` from GitHub (about 190 KB, checked against its published SHA-256)
  or to show the folder it belongs in, `UIFramework\lib\<version>\` next to Streamer.bot. Nothing is fetched
  without that click. When a newer UIFramework is published, opening the window offers it once: *Yes* downloads,
  *No* asks again next time, *Cancel* skips that version.
- **The window is built from the game's own settings table.** The game declares every setting once and answers the
  window's `uiframework.describe` request with it, so the window and the game can never disagree about a key, a
  default or a range again.
- **The word banks are edited in place.** All three sit on the Word banks page, each with *Add row* and *Restore
  defaults*, still in `RT-wordbank.json`, the file the game and the battle read. Empty rows are dropped on save.
- **Customise mode.** The pencil at the bottom left lets you rename, reorder, hide and move pages and fields by drag
  and drop or from the context menu, and pick the accent colour. It lives in `uiframework.layout.json` next to
  `RT-settings.json` and survives every import of the game.
- `RT-settings.json` keys are camelCase now (`useBot`, `minBet`, `globalCooldown`, `overlayAccentColour`). An
  existing file keeps working: the old names are read through aliases, and the first save writes the new ones.
- Light/dark and the rainbow mode live in `uiframework.layout.json` and are shared with every other window built on
  UIFramework. An existing `DarkMode` is taken over on the first open.
- Values typed out of range are pulled back into range when the game reads them, not only when the window saves.
- The overlay page is carried by the `RhymeTime Game` action now and written when the window asks for it (copying
  the URL, the demo, the OBS setup) or when a round with the overlay on finds it missing.
- Closing the window with unsaved changes asks first, from Cancel and from the title bar's X alike; a recompile or
  shutdown in Streamer.bot closes it without asking.

### Fixed

- **A damaged `RT-wordbank.json` is no longer quietly thrown away.** The game sets the damaged file aside as
  `RT-wordbank.json.broken`, falls back to the `.bak` from before the last save, and never writes the shipped words
  over a file somebody typed into. The window shows the defaults for that bank until you save.

### Removed

- The window's own WPF code and update check (about 4,500 lines) left the import; the DLL carries them now.

## [1.1.0] - 2026-10-30

### Added

- **An OBS overlay.** A browser source that shows the round on stream: the word with its ending
  picked out, the countdown, the attempts left, and then the rhyme that won it and what it paid, or
  the examples after a lost one. Battles get the same card in their own colour. It ships inside the
  import — the new **Overlay** page writes the page out, copies the URL for OBS and opens a demo
  that plays sample rounds — and it listens to Streamer.bot's own WebSocket server, so there is
  nothing extra to download or install. Off until you switch it on.
- **One button sets the overlay up in OBS.** Over Streamer.bot's OBS connection it creates the scene
  and puts a browser source in it, the size of your canvas, pointed at the overlay. A source name
  OBS already knows is left alone rather than overwritten.
- **The overlay is yours to style from the window.** Where the card sits, how big it is, how long a
  result stays up, whether it shows the ending, the attempt dots, the stake and the rhymes after a
  loss, and four colours with a picker behind each swatch. All of it travels with the round, so a
  change is on screen the next time somebody plays and OBS is never touched again. The Browser
  source's own Custom CSS is still read afterwards and still wins.

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
