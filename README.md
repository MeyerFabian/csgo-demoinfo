# csgo-demoinfo
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
