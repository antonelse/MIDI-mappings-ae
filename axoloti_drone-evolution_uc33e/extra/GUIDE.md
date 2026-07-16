# AnDrone 🎛️ 

## Overview 🎯
Our goal is to control parameters of the AnDrone synthesizer, which runs on the Axoloti board, using the Evolution UC33e MIDI controller. Axoloti is a DIY-friendly digital audio environment for _“Sketching digital audio algorithms with the musical playability of standalone hardware.”_ It is open source and was created by the brilliant [Johannes Taelman](https://github.com/JohannesTaelman). [Here](https://www.youtube.com/watch?v=g9yBebl8-vk) the original presentation at the Chaos Computer Club ([CCC](https://www.youtube.com/@mediacccde)). The platform offers comprehensive sound design capabilities, which we can map to the UC33e's physical controls for more intuitive, hands-on manipulation. More info can be found [here](https://ksoloti.github.io/2-background.html).

![axo-board](./imgs/axoloti_banner.jpg) 
*The Axoloti Core board*

The AnDrone synthesizer was inspired by a patch from [Guilherme Martins](https://www.guilhermemartins.net/) ([original patch](https://github.com/guibot/DRONE-ENGINE)).

## Patch Analysis 🔍

![axo-drone-patch-osc_1-2-3](./imgs/osc_1-2-3.png)  

*AnDrone patch - Oscillators 1, 2, 3 section*

![axo-drone-patch-osc_4-5-6](./imgs/osc_4-5-6.png) 
 
*AnDrone patch - Oscillators 4, 5, 6 section*

![axo-drone-patch-misc](./imgs/misc.png)  

*AnDrone patch - I/O Stage, FX and Scale/Key section*

![axo-drone-patch-matrix](./imgs/matrix.png) 

*AnDrone patch - Matrix Mixer section*

#### Parameter Sections
There are few changes with respect to the V1:

* 6x Oscillators + ad‑hoc modulation 
* Filter section for each oscillator + ad‑hoc modulation
* Effects sections with reverb and delay acting on master
* 3x3 matrix mixer for more complex modulations
* Line Input (used for modulation)

For oscillator 1, 2, 4, 5 we use different synthesis models of the well known Mutable Instrument [Braids](https://pichenettes.github.io/mutable-instruments-documentation/modules/braids/) oscillator. You can easly change the synthesis models from the Axoloti patcher.

#### Matrix Mixer
We added additional signals for expand the modulation capabilities of the AnDrone.
We use a 3x3 matrix mixer with 3 different modulation as input that can be combine together to build a more complex modulation signals.
These modulations acts on Osc 4, 5 and 6.
The flow of the mixer could be better understood by looking the image below (P25 preset) and the patch above.
In specific:

- Input 
	- `src1` is a slow sine signal
	- `src2 ` is a slow ramp signal
	- `src3 ` is a random drift signal

- Output 
	- `out1` signal is summed with the `color` mod of OSC 4
	- `out2` signal is summed with the `color` mod of OSC 5
	- `out3` signal modulate alone the `pitch` of OSC 6

	
#### Line Input
The line input serves as an additional, but temporary, modulation signal of the cutoff frequency value of OSC 1, 2, 3. The signal is the source of an envelope follower.
The input is optimized for piezoelectric microphone, but you can adjust the gain stage directly on the patch.

#### Scale and Key
There are 46 possible scales to select, among the root key.
The pitch controls the pitch range of the oscillators. Therefore the range is important. 
Below a list of the int value and the relative octave extension.

Pitch control range (semitones):

- 24 (2 octaves) — good for a tight lead/melody
- 48 (4 octaves) — good general-purpose range for most melodic uses
- 60-72 (5-6 octaves) — covers most of a piano's usable range
- 128 (~10.7 octaves) — full range, spans from sub-audible to beyond audible pitch, too wide for most practical melodic use

In the Axoloti ecosystem, the oscillator frequency are summed to the pitch input. Therefore the built int frequency of the oscillator in this case acts as offset for the final frequency [WRITE BETTERE VERIFIYNG ON INTERNET].
These are some suggestions for setting the base frequency, considering that this will be summed to the pitch above.

Oscillator base frequency (knob):

- C1 ≈ 32.7 Hz — deep sub-bass
- C2 ≈ 65.4 Hz — bass
- C3 ≈ 130.8 Hz — bass / low melodic range
- C4 ≈ 261.6 Hz — "middle C", mid / melodic range
- C5 ≈ 523.3 Hz — lead / high range


The starting point base frequency (fixed) is:
- C1 for OSC 1, 3, 4
- C3 for OSC 2, 5
OSC 6 is noise therefore it does not have a this info.

## UC33e Mapping Configuration 🎹

The possible controls are nearly endless. For simplicity, I decided to divide the mapping into multiple pages (presets P23, P24 and P25 on the UC33e):

- **P23:** Source + Modulation + Filter + Mix sections for Osc 1, 2, 3
- **P24:** Source + Modulation + Filter + Mix sections for Osc 4, 5, 6
- **P25:** Effects + Matrix Mixer + Scale + Extra

| UC33e Presets | CC Range | Purpose |
|------|-----|-----|-----|
| **P23** | 1 - 33  | Source/Modulation | 
| **P24** | 67 - 99 | Source/Modulation |
| **P25** | 34 - 66 | Effects/Routing/Scale |

![uc33e_page_1](./imgs/uc33e_page_1.jpeg)  
*P22 preset*

![uc33e_page_2](./imgs/uc33e_page_2.jpeg)  
*P24 preset*

![uc33e_page_3](./imgs/uc33e_page_3.jpeg)  
*P25 preset*

## Changelog

- v.1.0.0
Base Config - 3 oscillator + modulations on several params of the oscillator and filters + effect

- v.1.1.0
Added 3 more oscillator + modulation matrix for the latest added oscillators

- v.2.0.0
Added the possibility to modulate the first 3 oscillators' filters' cutoff using mic input (optimised for piezo)

- v.2.1.0
Added key quantisation. The oscillators follow a specific selectable scale

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
- Add crunchiness on delay path
- Optimize CPU usage
- add LFO with multiple squares
- add second piezo on the R channel for more modulation
- Add more informative compressor control
- Add soft clipping stage after filter stage or summing stage
- midi clock in to clock LFOs
- use the 2 selector that are on the Axo 
- for now the leds are linked to the first LFO signal. Thing about other uses.

## AxoLove ❤️
![axoloti_board](./imgs/axoloti_core_v1.2.jpg)  
*My Axoloti Core board v1.2*

![axolotl](./imgs/axolotl.webp)  
*The real Axolotl <3*