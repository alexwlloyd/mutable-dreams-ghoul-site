# Mutable Dreams 1.1 + GHOULBOX grit (unofficial build)

Mutable Dreams' sequencer, Biomes, phrases and granular bus are unchanged. This build adds
the larger, grittier sound of [GHOULBOX](https://github.com/jasonpersinger/ghoulbox-fm1-dungeon-synth)
(dungeon-synth firmware for the M-VAVE FM-1), ported to Mutable Dreams' float engine.
This is not an official Mutable Dreams or GHOULBOX release.

## What's new

**Two engines** (ALGO, after Satin Morph):

| Engine | K1 | K2 | K3 | From GHOULBOX |
| --- | --- | --- | --- | --- |
| **GHOUL GURDY** | WHEEL: bow pressure, brightness, rosin noise | DRONES: bourdon on the Biome root, then the pure fifth above (from 50 %) | BUZZ: the trompette, kicked on eighth-note wrist strokes | `eng_gurdy.c` |
| **GHOUL ANALOG** | DRIVE into a soft clipper | WAVE: SAW / SQUARE / PWM / SYNC / SUB | DETUNE, WIDTH, SYNC sweep (0-24 st) or SUB level | `eng_analog.c` |

The gurdy's drones ring through the rests while the transport runs (GHOULBOX's RING), so a single
track holds a drone under the melody. Both engines use the track's own Mutable Dreams filter,
envelope, Tides, Warps, sends and phrases.

**GRIT / HALL page** (EDIT, after Global Mixer; browser: "EDIT 6 · Grit / Hall"):

- **K1 DRIVE** (per track, every engine): GHOULBOX's DIST: a ~55 Hz split, drive up to 9x into an
  asymmetric soft clip, a tone low-pass that closes with drive. The low band under the split is
  added back clean, so kicks and drones keep their weight.
- **K2 CRUSH** (per track): sample-rate (1-16x) and bit reduction (15 down to 4 bits).
- **K3 SPACE** (global): ROOM (the 1.1 room and echo) or **HALL**, Jon Dattorro's plate tank as in
  GHOULBOX 2.x. FX › SPACE's tail knob sets its decay (about 1.5 to 12 s). HALL uses the echo's
  memory, so the echo is silent while HALL is on.
- **K4 HALL DAMP** (global): darker tail.

**48 sounds** (PRESET ids 224-271): 16 gurdies (Hurdy Gurdy, Drone Wheel, Bagpipe, Plague Cart,
Iron Bourdon…), 16 analog voices (Crypt Pad, War Horn, Dirge Bass, Sync Scream, Sub Rumble…), and
16 gritty voices for the original engines (Tomb Kick, Iron Boom, Rusted Snare, Chain Hat, Bowed
Iron, Dungeon Harp, Grim Tuba, Black Bell…). GHOULBOX sounds bring their DRIVE/CRUSH; other sounds
leave the track's grit as it is.

**8 Biomes** (77-84, family Dungeon & Crypt): Crypt Procession, Tomb of Ash, Plague Tavern, Iron
Monastery, Frozen Keep, Black Banner, Wraith Marsh, Siege Engine.

The 77 factory Biomes and 224 sounds of 1.1 render bit-identically (checked by the DSP test's
per-Biome hashes) until you turn grit on.

## Compatibility

- The patch format is now version 7 (1,356 bytes). 1.1 patches, saved Biomes, User Biome slots
  and `.mddb` backups load and migrate (grit off, ROOM). Exported 1.1 JSON patches import.
- Going back to the official 1.1 firmware: Biomes and User Biome slots saved with this build
  read as invalid there. Back up first (`.mddb`) as Recovery-1.1.txt describes.
- User Sound slots keep their 1.1 layout and do not store DRIVE/CRUSH.
- The package keeps the 1.1 identity (FM-1_710010100) so the 1.1 live editor connects.

## Not verified on hardware

Built with the exact 1.1 toolchain (`jieli-linux-toolchains-20260730.1`) and passes the platform's
build checks (image, RAM, pool headroom, no soft-double), the DSP, feature, quality and UI test
suites, and the browser engine test. **It has not been run on a physical FM-1.** The ECO admission
weights for the new engines, DIST/CRUSH and HALL are estimates. If a dense Biome crackles, set
GLO › SYSTEM › QUALITY to ECO, mute a track, or remove some drive. Install with
`python3 base/tools/fm1_install.py --yes Mutable-Dreams-1.1-Ghoul.fwsc`; recovery is the same as
for 1.1 (reinstall the official 1.1 package or Stock V15).

## Building

As BUILDING.md, plus: `python3 tools/generate_ghoulbox.py` after `tools/generate_presets.py`
(it writes `app/dsp/ghoul_bank.inc` and extends `presets/catalog.json`). The three AC79 SDK
packaging files were recovered from the released 1.1 `.fwsc` and match the SHA-256 values
`base/tools/build.py` requires.

## Licence and credits

GPL-3.0-only as a whole. GHOULBOX by Jason Persinger, on Felucca by Leo Kuroshita / Hügelton
Instruments (GPL-3.0-only); Mutable Dreams by its contributors; Plaits, Rings, Elements and stmlib
by Émilie Gillet / Mutable Instruments (MIT). HALL after J. Dattorro, "Effect Design, Part 1",
JAES 1997.
