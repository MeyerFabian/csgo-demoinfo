# csgo-demoinfo nade extractor
Rewrote [demoinfogo](https://github.com/ValveSoftware/csgo-demoinfo) to extract all nades thrown in a demo into a csv format: [Example](https://github.com/MeyerFabian/csgo-demoinfo/blob/master/nades-starladder-berlin-2019-mouse-vs-avangar-inferno.csv) (mouz-vs-avangar).

The demo viewer can be sometimes tedious to work with i rewrote demoinfogo a little bit. Demoinfogo parses the whole demo event-by-event and can output pretty much everything: Footsteps, Nades, Death, Damage etc.

I focused on just outputting all nades in a match into an easy-to-work copy-paste into ingame-console format. This is for instance [Ropz INSANE smoke to delay Avangar taking banana control on Inferno](https://www.reddit.com/r/GlobalOffensive/comments/culws2/ropz_insane_smoke_to_delay_avangar_taking_banana/):

`setpos 2094.015625 -111.995995 128.030380; setang 343.064575 153.105469 0.0`

You can just paste it into console with `sv_cheats` on and you will be teleported to the exact position and mouse position. Keep 128 tick in mind and that it is a jumpthrow.

## How do i execute this?
  * Download the latest [release](https://github.com/MeyerFabian/csgo-demoinfo/releases) (or build from source).
  * Open up the console where you put demoinfogo.exe. (Shift-Rightclick in the corresponding window -> Open Powershell Window). Type:

`.\demoinfogo.exe path-to-demo.dem -nades -roundinfo >> output_file.csv`

This takes some time as demoinfogo is not exactly programmed for speed or high usability. You will have generated an output_file.csv that looks like [this](https://github.com/MeyerFabian/csgo-demoinfo/blob/master/nades-starladder-berlin-2019-mouse-vs-avangar-inferno.csv). If you don't want to have round events (round start, round end, scores,half time) just leave out `-roundinfo`.

## How do i use this?
  * **With Demo Viewer**: Pause when a nade is thrown that you want to know how to throw and note the time (or tick). After you have finished the demo you can just lookup the time in the output_file.csv and copy the setpos ; setang;. For instance for the ropz nade you would type down: 1h 30m 21s. Here is the line in the [csv](https://github.com/MeyerFabian/csgo-demoinfo/blob/master/nades-starladder-berlin-2019-mouse-vs-avangar-inferno.csv#L636) (the very top).
  * **With Stream**: Note down score and time in the round, then you can hopefully easily look it up with -roundinfo. For instance the ropz nade above was thrown at 1:20m at a score of 15:13. Here is the line in the [csv](https://github.com/MeyerFabian/csgo-demoinfo/blob/master/nades-starladder-berlin-2019-mouse-vs-avangar-inferno.csv#L636) (the very top).
  * **On its own**: This can be useful, just because it puts you of the context of the game. Now you only concentrate on the nade thrown. I found that you tend to think more about "trivial" nades like anti-aggression flashes. E.g. i saw frozen on inferno t-side bounce an anti-agression flash from false-mid to mid to counter early ct mid aggression. Such a nade in a stream or demo is so trivial that you basically overlook it, especially if there was no aggression from the cts in the first place.

You can open up the csv file with excel, openoffice calc or any other program that creates simple tables.

### FAQ:

  * **Does it recognize jump/walk/run throws?** No, in most cases you will find out pretty quickly if its one of those.
  * **Does this replace/speed up the demo viewer?** No. You may save on some rewinds if you note down the time of for instance an execute. You can go into the csv-file and see all nades thrown at that time and directly hop into game and cycle through the nades thrown at that time.
  * **Why are demos slow?** My guess: Demos are event-based and don't store an intermediate match state. This means if you rewind the demo viewer, it needs to go through the whole demo again. This is also why rewinding at the start of the game doesn't take as much time as later in the game. The demo viewer could generate intermediate state probably and delete if you stop watching the demo but it simply doesn't do it.
  * **Do you plan on extending on this?** Only small bug fixes else i would rewrite the whole thing.

### Problems:
  * **Score might be displayed wrongly:** Demos and demoinfogo are event-based. Some tournament organizers cut off the event round_announce_match_start which officially starts the match and resets score. It also might not recognize if a round that is being played is not 'live' and ends but doesn't contributes to the score. The Example demo has matchmaking medic (round 5) and everything is displayed right. Luckily, the demo ends the round in question with a draw which i can recognize. So be aware that there could be more cases where it occurs.
  * **Round time is hardcoded:** afaik tournament and matchmaking round times are synchronized, so should not make a difference. Somehow the timelimit always returned 0. So i hardcoded that a round takes 115s beginning with the end of freeze time (so timeouts should work as well).
