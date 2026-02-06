# MIDI Setup 🎛️

## Overview 🎯
Our goal is to control parameters of the AxoDrone synthesizer, which runs on the Axoloti board, using the Evolution UC33e MIDI controller. Axoloti is a DIY-friendly digital audio environment for _“Sketching digital audio algorithms with the musical playability of standalone hardware.”_ It is open source and was created by the brilliant [Johannes Taelman](https://github.com/JohannesTaelman). [Here](https://www.youtube.com/watch?v=g9yBebl8-vk) the original presentation at the Chaos Computer Club ([CCC](https://www.youtube.com/@mediacccde)). The platform offers comprehensive sound design capabilities, which we can map to the UC33e's physical controls for more intuitive, hands-on manipulation. More info can be found [here](https://ksoloti.github.io/2-background.html).

![axo-board](./imgs/axoloti_banner.jpg) 
*The Axoloti Core board*

The AxoDrone synthesizer is a custom patch created by [Guilherme Martins](https://www.guilhermemartins.net/) and adapted by me.  
The original patch is available on his personal GitHub [here](https://github.com/guibot/DRONE-ENGINE) and is free to use.

## Version Specs 📚
At the time of writing, I developed 2 different versions of the AxoDrone synthesizer, v1 and v2.
Here some specs about the preset number, CC range of the UC33e controller in addition to the related versions matching.

| UC33e Presets | CC Range | AxoDrone Ver. | Purpose |
|------|-----|-----|-----|
| **P22** | 1 - 33  | v1/v2 | Source/Modulation | 
| **P23**| 34 - 66 | v1 | Effects/Routing | 
| **P24** | 67 - 99 | v2 | Source/Modulation |
| **P25** | 34 - 66 | v2 | Effects/Routing |


## AxoDrone V1
### Patch Analysis 🔍

![axo-drone-patch-v1](./imgs/axoloti_drone_patch_v1.png)  
*AxoDrone v1 patch*

#### Parameter Sections:
The patch is primarily composed of:

* 3x Oscillators + ad‑hoc modulation and mixing stages
* Line input
* 2x Independent effects sections (one for the 3 oscillators, one for the line input) with reverb and delay
* Filter section for each oscillator
* MIDI input with ASR controlling the oscillators' pitch

### UC33e Mapping Configuration 🎹

The possible controls are nearly endless. For simplicity, I decided to divide the mapping into two pages (presets P22 and P23 on the UC33e):

- **P22:** Source + Modulation + Filter + Mix sections
- **P23:** Effects + LineIn + MIDI

![uc33e_page_1](./imgs/uc33e_page_1_v1.jpeg)  
*P22 preset*

![uc33e_page_2](./imgs/uc33e_page_2_v1.jpeg)  
*P23 preset*

## AxoDrone V2
### Patch Analysis 🔍

![axo-drone-patch-v2](./imgs/axoloti_drone_patch_v2.png)  
*AxoDrone v2 patch*

#### Parameter Sections:
There are few changes with respect to the V1:

* 3x more Oscillators + ad‑hoc modulation and mixing stages, for a total of 6 Oscillators
* 3x3 matrix mixer for more complex modulations
* NO Line input
* NO MIDI input

We replaced Oscillator 1, 2, 4, 5 with different synthesis models of the well known Mutable Instrument [Braids](https://pichenettes.github.io/mutable-instruments-documentation/modules/braids/) oscillator. You can easly change the synthesis models from the Axoloti patcher.

#### Matrix mixer details:
In the v2 we added additional signals for expand the modulation capabilities of the AxoDrone.
We use a 3x3 matrix mixer with 3 different modulation as input that can be combine together to build a more complex modulation signals.
These modulations acts on Osc 4, 5 and 6.
The flow of the mixer could be better understood by looking the image below (P25 preset) and the patch above.
In specific:

- out1 signal is summed with the timbre mod of Osc 4
- out2 signal is summed with the timbre mod of Osc 5
- out4 signal modulate alone the pitch of Osc 6

### UC33e Mapping Configuration 🎹

I decided to divide the mapping into 3 pages (presets P22, P24 and P25 on the UC33e):

- **P22:** Source + Modulation + Filter + Mix sections for Osc 1, 2, 3
- **P24:** Source + Modulation + Filter + Mix sections for Osc 4, 5, 6
- **P25:** Effects + Matrix Mixer + Extra

**Important Notes**:

- **P22** is the same as V1. Please refer to the V1 image for this page.
- We do not use **P23**, since was already used in V1.


![uc33e_page_3](./imgs/uc33e_page_3_v2.jpeg)  
*P24 preset*

![uc33e_page_4](./imgs/uc33e_page_4_v2.jpeg)  
*P25 preset*

## Resources 📚
- [1] [Axoloti article on CDM](https://cdm.link/axoloti-makes-any-music-hardware-you-can-imagine/)
- [2] [Axoloti presentation](https://www.youtube.com/watch?v=g9yBebl8-vk)
- [3] [Axoloti Factory Objects](https://www.privatepublic.de/public/factory-objectlist.html) [discontinued]
- [4] [Ksoloti (new Axoloti)](https://ksoloti.github.io/index.html) [the deserving successor of the discontinued Axoloti core board]
- [5] [Ksoloti discussion on MW](https://www.modwiggler.com/forum/viewtopic.php?t=277847&start=810)
- [6] [Ksoloti community](https://ksoloti.discourse.group/)
- [7] [Ksoloti Github repo](https://github.com/ksoloti)
- [8] [Guilherme on Drone patch](https://www.youtube.com/watch?v=osG7fh6tiE8) 
- [9] [Drone original patch](https://github.com/guibot/DRONE-ENGINE/commits?author=guibot)
- [10] [Peeps Music Box by s8jfou](https://www.s8jfou.com/synth.html) | [Video](https://www.youtube.com/watch?v=w7IrjJ7MmoY)
- [10] [M-Audio Evolution UC33e Manual](https://www.strumentimusicali.net/manuali/M_AUDIO_UC-33e_EN.pdf)

## TODO List 📝
- Understand MSB and LSB parameters for higher resolution control
- Think about the addition of the play/pause/fwd buttons in the bottom right (burst like modulation ?)
- Add crackle noise
- Optimize CPU usage
- Add more informative compressor control

## AxoLove ❤️
![axoloti_board](./imgs/axoloti_core_v1.2.jpg)  
*My Axoloti Core board v1.2*

![axolotl](./imgs/axolotl.webp)  
*The real Axolotl <3*