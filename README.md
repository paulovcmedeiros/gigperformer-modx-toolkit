# Vini’s Gig Performer MODX Toolkit

Unofficial GPScript, scriptlet, example, and documentation toolkit for using
Gig Performer as a MIDI control surface and automation layer for Yamaha MODX.

The main idea is simple:

- Yamaha MODX produces and processes the sound.
- Gig Performer manages live control, MIDI routing, widgets, songs, rackspaces,
  variations, and scripted behavior.
- GPScript and scriptlets provide deterministic MIDI and SysEx logic where plain
  widget mappings are not enough.

This project is developed from a real live-rig workflow, but this repository
contains only the reusable parts: scripts, scriptlets, examples, notes, and
minimal demo gig files.

## Status

Early public extraction. APIs, widget contracts, file names, and examples may
change.

Tested primarily with:

- Yamaha MODX7, original MODX generation
- MODX firmware 2.52.0
- Gig Performer Pro 5.2.2
- macOS on an Intel MacBook Pro

Other MODX, MODX+, MONTAGE, or Gig Performer versions may work, but are not yet
systematically tested.

## What is included

### GPScript

Reusable GP scripts and scriptlets live under [`gpscript/`](gpscript/):

```text
gpscript/
  gig-scripts/
  rackspace-scripts/
  scriptlets/
```

Current planned components include:

- MODX Performance and Part name display
- MODX Part on/off status reflection
- deterministic MIDI CC sending
- Hammond/drawbar-style MODX control helpers
- song-change trigger helpers
- MIDI splitting, octave, sustain, and routing utilities

### Examples

Minimal example gig files live under [`examples/`](examples/).

The examples are intentionally small. They are meant to demonstrate one idea at
a time, not to reproduce a full personal live rig.

### Documentation

Documentation lives under [`docs/`](docs/).

Important documents:

- [`docs/setup.md`](docs/setup.md)
- [`docs/compatibility.md`](docs/compatibility.md)
- [`docs/widget-contracts.md`](docs/widget-contracts.md)
- [`docs/modx-midi-settings.md`](docs/modx-midi-settings.md)
- [`docs/modx-sysex-notes.md`](docs/modx-sysex-notes.md)
- [`docs/troubleshooting.md`](docs/troubleshooting.md)

## Core concepts

### Widgets are UI/state

Gig Performer widgets are useful as visible state, live controls, and links to
rackspace/variation data.

For some workflows, especially batch updates or preset-driven control, relying
on widget MIDI output alone may not be deterministic enough.

### Scripts and scriptlets perform the actual MIDI work

For repeatable behavior, this toolkit favours explicit GPScript/scriptlet logic:

- receive widget changes;
- scale values;
- construct MIDI CC, PC, or SysEx messages;
- send them to the intended MIDI output block;
- optionally reflect hardware state back into widgets.

### MODX state can be reflected back into GP

Some scripts parse incoming MODX SysEx replies and use them to update GP
widgets. For example, a rackspace can display the current MODX Performance name
and the names of active Parts.

These SysEx formats are based on observed behavior and should be treated as
working notes unless explicitly tied to Yamaha documentation.

## Installation

At this stage, installation is manual.

1. Clone or download this repository.
2. Copy the relevant `.gpscript` file into your Gig Performer script/scriptlet
   workflow.
3. Create the required widgets and MIDI blocks described in the corresponding
   example or widget contract.
4. Adapt MIDI block names and widget handles as needed.
5. Test with the GP MIDI Monitor and the MODX before using live.

## Repository layout

```text
gigperformer-modx-toolkit/
  gpscript/
    gig-scripts/
    rackspace-scripts/
    scriptlets/

  examples/
    minimal-part-name-display/
    hammond-drawbars/
    deterministic-cc/

  docs/
    setup.md
    compatibility.md
    widget-contracts.md
    gp-architecture.md
    modx-midi-settings.md
    modx-sysex-notes.md
    troubleshooting.md

  references/
  tools/
```

## Naming conventions

This repository uses lower-case, hyphen-separated file names where practical.

Examples:

```text
modx-performance-part-labels.gpscript
song-change-toggle-osc-trigger.gpscript
modx-hammond-drawbars.gpscript
```

Inside Gig Performer, widget handles may still use GP-style names such as:

```text
PerformanceNameWidget
PartLabel01
PartLabel02
LiveSetSelectorBank
```

The required widget handles for each script are documented in
[`docs/widget-contracts.md`](docs/widget-contracts.md).

## Safety and live-use warning

Test everything before using it live.

This toolkit can send MIDI CC, Program Change, and SysEx messages to external
hardware. Incorrect routing or incorrect values can change MODX state in ways
you did not intend.

Recommended testing workflow:

1. Test in a duplicate Gig Performer gig file.
2. Use GP MIDI Monitor.
3. Use a backup MODX Performance or Live Set.
4. Confirm MIDI routing before enabling automatic song/variation behavior.

## Compatibility

Known primary target:

```text
Yamaha MODX7, firmware 2.52.0
Gig Performer Pro 5.2.2
```

The code may be useful with MODX+, MONTAGE, or related Yamaha instruments, but
that should be considered experimental unless documented otherwise.

## Contributing

Contributions, bug reports, observations, and tested compatibility reports are
welcome.

Useful reports include:

- MODX/MODX+/MONTAGE model;
- firmware version;
- Gig Performer version;
- operating system;
- MIDI connection type;
- exact script/example used;
- what worked;
- what failed;
- GP log or MIDI monitor output when relevant.

## License

MIT License, unless otherwise stated.

## Disclaimer

This project is unofficial and is not affiliated with Yamaha, Deskew
Technologies, or Gig Performer.

Yamaha, MODX, MONTAGE, Gig Performer, and related names belong to their
respective owners.
