# Paulo Medeiros' Gig Performer Toolkit for Yamaha MODX

Small collection of GPScript files I use with Gig Performer and a Yamaha MODX.
The focus is MIDI routing/control, a few scriptlets, and some MODX SysEx helpers.

This project is unofficial and is not affiliated with, endorsed by, or sponsored
by Yamaha, Deskew Technologies, or Gig Performer. It is mostly code from my own
setup that may also be useful to other GP/MODX users.

## Status

Early and personal. File names, widget assumptions, and script behavior may
change as I keep cleaning this up from my own live-rig workflow.

Tested primarily with:

- Yamaha MODX7, original MODX generation
- MODX firmware 2.52.0
- Gig Performer Pro 5.2.2
- macOS on an Intel MacBook Pro 2015

Other MODX, MODX+, MONTAGE, or Gig Performer versions may work, but I have not
tested them. Wish I had them to test :)

## What's Here

```text
gpscript/
  scriptlets/
  gig_scripts/
  rackspace_scripts/
  MODX/
  GeneralUtils/
```

### Scriptlets

The scriptlets are standalone GP scriptlets:

- `assignable_function_buttons.gpscript`: send MODX AF1/AF2 state per MIDI channel.
- `keyboard_splitter.gpscript`: create split zones per MIDI channel.
- `midi_channel_faders.gpscript`: send MIDI volume changes per channel.
- `midi_channel_octaver.gpscript`: transpose notes by octave per MIDI channel.
- `midi_channel_selector.gpscript`: allow or mute MIDI by channel.
- `midi_channel_selector_sustain.gpscript`: route sustain by channel with optional auto-sustain.
- `modx_performance_selector.gpscript`: select MODX Live Set performances and sync names.
- `note_velocity_monitor.gpscript`: show per-channel note velocity values.

### Gig and Rackspace Scripts

- `gig_scripts/song_change_toggle_osc_trigger.gpscript`: toggles an OSC value when the song changes.
- `rackspace_scripts/MODX_Toolkit_RackspaceScriptTemplate.gpscript`: example rackspace script that receives MODX SysEx and updates performance/part labels.

### Include Files

The `MODX/` and `GeneralUtils/` folders contain reusable include files used by
the rackspace template and available for MODX-related scripts. They are not
meant to be loaded as standalone scripts.

## Using The Files

At this stage, installation is manual:

1. Put this repository directory under the folder Gig Performer uses as the root
   for GPScript `Include` paths.
2. Keep the directory name as `gigperformer-modx-toolkit`, or update the
   `Include` paths in the scripts.
3. In the relevant Gig Performer script or scriptlet editor, add an `Include`
   line for the file you want to use, for example:

   ```gpscript
   Include "gigperformer-modx-toolkit/gpscript/scriptlets/keyboard_splitter"
   ```

4. Create any required widgets and MIDI blocks with the names expected by the script.
5. Test with GP MIDI Monitor before using it live.

The include paths currently expect this layout:

```text
<Gig Performer include root>/
  gigperformer-modx-toolkit/
    gpscript/
      GeneralUtils/
      MODX/
      ...
```

Some files assume specific widget handles, MIDI block names, or MODX settings.
Those assumptions are currently documented mostly in the scripts themselves.

## Safety

These scripts can send MIDI CC, Program Change, OSC, and SysEx messages. Test in
a duplicate gig file and use a backup MODX Performance or Live Set while trying
things out.

## Disclaimer

Yamaha, MODX, MONTAGE, Gig Performer, and related names belong to their
respective owners.
