# Hades Music VMC-207 — Reason Remote Codec

Deprecated Reason Remote files (Lua codec + remote map) for using the Hades Music VMC-207 MIDI controller as a controller for Reason's Main Mixer. No longer in development; kept here as an archive.

The codec, map and SysEx preset are my own work, written 2017–2018.

The codec also includes code for using the VMC-207 together with a **Doepfer Drehbank** knob controller on the same surface (see below). If you don't have a Drehbank, you may want to remove that code.

## Controls

**VMC-207**
- 16 channel strips (MIDI channels 1–16): Fader (CC 7), Pan (CC 10), Select (CC 9), Mute (CC 12, with LED feedback) and Solo (CC 13)
- Master Fader, 4 Gain + 4 Q encoders
- Transport (Stop, Play, Rec, Back, Forward), arrow keys, Plus/Minus, Jog button

**Doepfer Drehbank** (optional)
- 128 knob items: 8 CCs (15, 18, 21, 24, 27, 30, 40, 43) on each of the 16 MIDI channels

## Supported devices

**Reason Document**

| Control | Reason |
|---------|--------|
| Stop / Play / Rec | Stop / Play / Record |
| Back / Forward | Move Loop Left / Right |

**Reason Master Section** (the Main Mixer, 16 channels per bank)

| Control | Reason |
|---------|--------|
| Fader 1–16 | Channel Level |
| Mute / Solo 1–16 | Channel Mute / Solo |
| Select 1–16 | Choose which channel the Drehbank knob grid edits |
| Master Fader | Control Room Level |
| Arrow Left / Right | Previous / Next bank of channels |
| Arrow Up / Down | Previous / Next Insert FX patch (selected channel) |
| Minus / Plus | All Mutes Off / All Solos Off |

With a Drehbank, for the **selected channel**, knob columns 1–8 give a full channel strip: EQ gain, frequency and Q, HPF/LPF, the insert Rotary 1–4, FX sends, input gain, and the gate and compressor. Knob columns 9–16 stay fixed on channels 13–16 (insert Rotary 1–4 and EQ gains).

## Using it without a Doepfer Drehbank

Everything named `Knob 1`–`Knob 128` belongs to the Drehbank. The VMC-207 works without it, but those items will still show up in Reason and their mappings will do nothing. To remove the Drehbank code:

1. In `Hades VMC-207.lua`, delete the `Knob 1`–`Knob 128` lines from the `items` table (the `-- BANK 1` / `-- BANK 2` blocks) and from the `inputs` table.
2. In `Hades VMC-207.remotemap`, delete every `Map` line whose first column is `Knob …` (the `// SENDS` block and the knob lines inside each `CH1`–`CH16` group), so the map doesn't refer to items that no longer exist.

Without the Drehbank, Select 1–16 still choose a channel, but only Arrow Up/Down (Insert FX patch) act on it.

## Files

- `Hades - Sysex - Single USER.syx`: a SysEx preset for the VMC-207.
- `Manuals/`: the VMC user manual from Hades Music (Spanish PDF, English as photographed pages), included for reference.

## Install

1. Copy `Hades VMC-207.luacodec`, `Hades VMC-207.lua` and `Hades VMC-207.png` to the `Remote/Codecs/Lua Codecs/Hades/` folder.
2. Copy `Hades VMC-207.remotemap` to the `Remote/Maps/Hades/` folder.
3. Restart Reason, then add the surface manually in Preferences → Control Surfaces (Manufacturer: Hades, Model: VMC-207).

On macOS the Remote folder is `~/Library/Application Support/Propellerhead Software/Remote/`; on Windows it's `%APPDATA%\Propellerhead Software\Remote\`.

## Licence

MIT — see `LICENSE`. This covers the codec, map and SysEx preset. The manuals in `Manuals/` belong to Hades Music and aren't covered by this licence.
