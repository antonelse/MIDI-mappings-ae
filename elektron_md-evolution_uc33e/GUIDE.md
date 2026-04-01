# MIDI Setup 🎛️

## Overview 🎯
Our goal is to control some parameters of the Elektron Machinedrum (MD). 
Specifically, we focus on the **DATA ENTRY** knobs (synthesis, effects, routings) used for tweaking machine parameters, plus the **LEVEL** (volume) knob of each machine [1].

For each of the 16 machines we have 24 different DATA ENTRY knobs:

* 🎛️ 8 for Synthesis - 1st MD page
* 🔥 8 for Effects - 2nd MD page  
* 🔗 8 for Routing - 3rd MD page
* 🔊 16 LEVEL knobs, one for each machine

![md](./imgs/md.png)

For this configuration, we suggest using a **Control Base Channel** = 1-4, which can be selected in the GLOBAL configuration of the MD.

The CTRL-CHANGE mappings follow these rules [1]:
![mapping_1](./imgs/mapping_1.png)

## MIDI Channel Mapping 📡

**MIDI CHANNEL 1** — Controls machines 1, 2, 3, 4:

- **Machine 1**: 
  - LEVEL knob: 8
  - MUTE button: 12
  - DATA ENTRY knobs: 16 → 39
- **Machine 2**: 
  - LEVEL knob: 9
  - MUTE button: 13
  - DATA ENTRY knobs: 40 → 63
- **Machine 3**: 
  - LEVEL knob: 10
  - MUTE button: 14
  - DATA ENTRY knobs: 72 → 95
- **Machine 4**: 
  - LEVEL knob: 11
  - MUTE button: 15
  - DATA ENTRY knobs: 96 → 119

**MIDI CHANNEL 2** — Controls machines 5, 6, 7, 8  
**MIDI CHANNEL 3** — Controls machines 9, 10, 11, 12  
**MIDI CHANNEL 4** — Controls machines 13, 14, 15, 16  

**💡 Note**: Only the MIDI CHANNEL changes - the CC values remain consistent across channels!

## UC33e Control Allocation 🎹
Due to this parameter configuration, we can divide the UC33e as follows:
![uc33e](./imgs/uc33e-data_entry.jpg)

You can see that each MD page of the DATA ENTRY section fits perfectly in a single row of the UC33e. In other words, the 3 pages of the MD can be entirely mapped to the 3 rows of the UC33e. 

Since the UC33e can store multiple presets (up to 33), we can assign **1 UC33e preset for each MD machine**. This way, by recalling/loading each preset, we can edit a single machine on our MD.

We end up with **16 different presets**, from P01 to P16.

**➕ Additionally**, we create preset P17 where we map all LEVEL knobs and MUTE buttons for all 16 machines.
![uc33e-custom](./imgs/uc33e-volumes.jpg)

### Fader Assignment:
- MD machines 1-8 VOLUME → Presets P01 to P08
- MD machines 9-16 VOLUME → Presets P09 to P16

## Mapping Procedure 🔄
For each parameter, we need to perform 2 main operations on the UC33e: **Assignment** and **Storage**.

I suggest performing the Assignment operation for **all** DATA ENTRY controls referring to a single MD machine, then storing the mapping to a single UC33e preset. 

### 1. Assignment:  
- Move the desired knob/fader/button 
- Press **ASSIGN**: Set the desired CC value for the MD (check CTRL-CHANGE MAPPINGS image) using the keypad
- Press **CHANNEL**: Set the desired MIDI Channel for the target MD machine

### 2. Storage: 
- Press **STORE**: Set the desired preset number where you want to save this mapping
- We choose to use P01 for MD machine 1, P02 for machine 2, and so on

**⚠️ Important**: Wait until the screen stops blinking before proceeding!

### Useful Tip 🔥

By looking at the MIDI implementation chart for the MD, we can notice a pattern of similarities among CCs across different machines. For this reason, I reported a similarity table below that shows which presets, i.e., P1 (MD machines), are similar in terms of MIDI settings. Each row lists the UC33e presets/machines that share the same MIDI implementation — the only difference is the MIDI channel.

| Ch 1 | Ch 2 | Ch 3 | Ch 4 | CC Range |
|------|------|------|------|----------|
| P1   | P5   | P9   | P13  | 16-39    |
| P2   | P6   | P10  | P14  | 40-63    |
| P3   | P7   | P11  | P15  | 72-95    |
| P4   | P8   | P12  | P16  | 96-119   |

**Example:**

P1 maps CC parameters from 16 to 39 on MIDI channel 1, which corresponds to a full mapping of MD machine 1 to the UC33e. P5, which maps MD machine 5, is identical — the only difference is the MIDI channel of the CCs. Therefore, copying (or better, saving) P1 into P5 and changing only the MIDI channel from 1 to 2 does the job, avoiding the need to redo the CC mapping from scratch.

**Note:** 

When performing the Copy/Paste operation, keep in mind the custom UC33e fader assignment mapping described before, as well as the CC implementation chart available in the MD manual:

1. Faders of UC33e presets from P1 to P8 controls MD machine from 1 to 8
	* Faders from P1 to P4 must be set to MIDI channel 1
	* Faders from P5 to P8 must be set to MIDI channel 2
2. Faders of UC33e presets from P9 to P16 controls MD machine from 9 to 16
	* Faders from P9 to P12 must be set to MIDI channel 3
	* Faders from P13 to P16 must be set to MIDI channel 4

## Workflow 🔄
As mentioned, we assign preset numbers (e.g., P03) to correspond with MD machines (e.g., machine 3, or *Track 3* in the manual[1]). Each UC33e preset stores mapping information for a single MD machine.

- **Load a Preset**: Press RECALL and enter the desired number (e.g., 3 for P03)
- **TBD** - Additional workflow steps to be defined

**⚠️ Important**: Wait until the controller's screen finishes blinking before using the controls!

## Resources 📚
- [1] [ELEKTRON Machinedrum Manual](https://www.strumentimusicali.net/manuali/ELEKTRON_SP1_ENG.pdf) - *Instant Classic!*
- [2] [M-Audio Evolution UC33e Manual](https://www.strumentimusicali.net/manuali/M_AUDIO_UC-33e_EN.pdf)

## TODO List 📝
- Check if P17 was mapped !
- Understand how to change predefined presets (1-4 upper right buttons)
- Understand MSB and LSB parameters (max MD resolution 32 bit)  
- Understand the PROGRAM parameter
- Understand the SELECT parameter
