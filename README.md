# Paulo Medeiros' Gig Performer Toolkit for Yamaha MODX

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
![Status: early](https://img.shields.io/badge/status-early-orange.svg)
[![Gig Performer](https://img.shields.io/badge/Gig%20Performer-tested%205.2.2-lightgrey.svg)](https://gigperformer.com)
[![Yamaha MODX](https://img.shields.io/badge/Yamaha-MODX-lightgrey.svg)](https://yamahasynth.com/learn/modx-series-synthesizers/introducing-the-modx-music-synthesizer)

This is a collection of reusable GPScript utilities and MODX helpers developed for my own Gig Performer/MODX live rig. The focus is MIDI routing and control, with the MODX as the sound engine and Gig Performer as its control layer.

The project reflects my own gigging needs and preferences, but I try to keep the scripts as reusable and general as my free time allows. I hope they are also useful to other GP/MODX users.

## Status

Early development. Public API changes and repo structure are still likely to occur.

## System Requirements

Tested primarily with:

- Yamaha MODX7 (original MODX generation, not the MODX+)
  - Firmware v2.52.0
- Gig Performer Pro 5.2.2

It may work for other Gig Performer and MODX versions, as well as for the MODX+ or MONTAGE
after targeted adaptations, but I have not tested them (wish I had them to test).

## Repository Contents

### Scriptlets

The files under `gpscript/scriptlets/` are meant to be used as standalone GP scriptlets:

- `assignable_function_buttons.gpscript`: send MODX AF1/AF2 state per MIDI channel.
- `keyboard_splitter.gpscript`: create split zones per MIDI channel.
- `midi_channel_faders.gpscript`: send MIDI volume changes per channel.
- `midi_channel_octaver.gpscript`: transpose or add octave layers per MIDI channel.
- `midi_channel_selector.gpscript`: allow or mute MIDI by channel.
- `midi_channel_selector_sustain.gpscript`: route sustain by channel with optional auto-sustain.
- `modx_live_set_selector.gpscript`: select MODX Live Set performances and request
  performance/part names. To display synced names in widgets, use it together
  with the MODX rackspace SysEx receiver/template.
- `note_velocity_monitor.gpscript`: show per-channel note velocity values.

### Gig and Rackspace Scripts

- `gig_scripts/song_change_toggle_osc_trigger.gpscript`: toggles an OSC value when the song changes.
- `rackspace_scripts/MODX_Toolkit_RackspaceScriptTemplate.gpscript`: example rackspace script that receives MODX SysEx and updates performance/part labels. Read the comments in the script for the widgets and MIDI block names you need to adapt.

### Include Files

The `MODX/` and `GeneralUtils/` folders contain reusable `Include` files used by
the rackspace template and scriptlets. They might also contain code that other fellow
GigPerformers may find useful.

## Using The Files

At this stage, installation is manual:

1. Put this repository directory under the folder Gig Performer uses as the root
   for GPScript `Include` paths.
   - On Windows, it's usually `C:\Users\<your user name>\Documents\Gig Performer\Scripts`
   - On Mac, it's usually `/Users/<your user name>/Documents/Gig Performer/Scripts`
2. Keep the directory name as `gigperformer-modx-toolkit`
3. In the relevant Gig Performer script or scriptlet editor, add an `Include`
   line for the file you want to use. For example:

   ```gpscript
   Include "gigperformer-modx-toolkit/gpscript/scriptlets/keyboard_splitter"
   ```
4. Some files assume specific widget handles, MIDI block names, or MODX settings.
   Those assumptions are currently documented mostly in the scripts themselves.
     - If applicable, create any required widgets and MIDI blocks with the expected names
     - This is usually not required for scriptlets
5. Compile the scripts or scriptlets you use in Gig Performer.

## Safety

These scripts can send MIDI CC, Program Change, OSC, and SysEx messages. Test in
a duplicate gig file and use a backup MODX Performance or Live Set while trying
things out.

## Getting in Touch

Feel free to get in touch here on GitHub should you need help or wish to contribute.

## Disclaimers

This project is personal and is not affiliated with, endorsed by, or sponsored
by Yamaha, Deskew Technologies, or Gig Performer.

Yamaha, MODX, MONTAGE, Gig Performer, and related names belong to their
respective owners.
