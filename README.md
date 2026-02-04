⚠️ **Disclaimer: Work in Progress STATUS** ⚠️

_This repository and its contents are currently a Work in Progress. Mappings, documentation, and file structures may be incomplete, subject to change, or contain inaccuracies. Use at your own risk and always verify critical settings with the official hardware manuals._

# MIDI-mappings-ae
A series of MIDI mappings I created for my studio # MIDI Mapping Repository 🎛️

*A collection of professional MIDI mappings for the Evolution UC33e controller with various hardware synthesizers and drum machines.*

---

## Overview

This repository contains comprehensive MIDI mapping configurations for the Evolution UC33e controller, providing hands-on control for electronic music production hardware. Each mapping is carefully designed to maximize workflow efficiency and creative potential.

## Available Mappings

| Device | Status | MIDI Channel | UC33e Presets | Controls | Documentation |
|--------|--------|--------------|---------------|----------|---------------|
| **Elektron Machinedrum** | ✅ Complete | 1-4 | P01-P17 | 33+ | [View Guide](./elektron_md-evolution_uc33e/GUIDE.md) |
| **Korg microKORG** | ✅ Complete | 5 | P20 | 36 | [View Guide](./microkorg-evolution_uc33e/GUIDE.md) |
| **Axoloti Drone** | ✅ Complete | 1 | P22-P22 | 33+ | [View Guide](./axoloti_drone-evolution_uc33e/GUIDE.md) |

## File Structure
```
MIDI-mappings-ae/
├── elektron_md-evolution_uc33e/
│   ├── GUIDE.md
│   ├── imgs/
│   └── dump.syx
├── microkorg-evolution_uc33e/
│   ├── GUIDE.md
│   ├── imgs/
│   └── dump.syx
├── axoloti_drone-evolution_uc33e/
│   ├── GUIDE.md
│   ├── imgs/
│   ├── extra/
│   └── dump.syx
├── controllers/
├── manuals/
├── complete_dump.syx
└── README.md
```
## UC33e-Related
### Mapping Process 🔄

For each parameter, perform these 2 main operations on the UC33e: **Assignment** and **Storage**.

#### 1. Assignment:
- Move the desired knob/fader/button to focus on it
- Press **ASSIGN**: Set the desired CC value using the keypad
- Press **CHANNEL**: Set the desired MIDI channel

#### 2. Storage:
- Press **STORE**: Set the desired preset number to save this mapping (e.g., 20 for P20)

**⚠️ Important**: Wait until the screen stops blinking before proceeding!

### Memory Dump/Restore 💾

Use [SysEx Librarian](https://www.snoize.com/SysExLibrarian/) software with a MIDI2USB cable for I/O communication. You can also send MIDI via USB by using the **MIDI OUT FROM USB** function (press SELECT + ASSIGN together).

#### Dump Process:
- Connect MIDI2USB to UC33e OUTPUT MIDI port
- In SysEx Librarian, select correct input source
- Press *Record Many* in SysEx Librarian
- On UC33e, press MEM.DUMP (DATA MSB + STORE)
- UC33e screen shows *SYS* - transmission in progress

#### Restore Process:
- Connect MIDI2USB to UC33e INPUT MIDI port
- In SysEx Librarian, select correct output source
- Select SysEx file and press *Play*
- UC33e screen shows *SYS* - receiving in progress

#### Load a Preset:
- Press RECALL and enter the preset number (e.g., 20 for P20)

### Useful Shortcuts 🎯
- **Reset UC33e**: Turn on while holding + and - buttons
- **Lock UC33e**: Press CTR MUTE (PROGRAM + DATA LSB)
- **Send Snapshots**: Press SNAPSHOT ("+" + "-")
- **MIDI Out via USB**: Press SELECT + ASSIGN together

### Useful Tips & Tricks 💡

**Speed Up MIDI CHANNEL Assignment:**

- Press CHANNEL button and quickly move each knob/fader one after another
- Use + and - buttons to adjust the value shown on screen
- UC33e remains in MIDI CHANNEL assignment mode during this process

**Speed Up CC Assignment:**

- Press ASSIGN and quickly move each knob one after another
- Enter the correct CC numbers on the keypad as you go

**Double-Check Assignments:**

- Quickly move knobs while watching the screen to verify CC and MIDI CHANNEL values

___

**MIDI-mappings-ae** - midi mappings. Copyright (C) 2025  Antonio Giganti - ae
