# Studio MIDI — Routing Reference

**Central hub:** CME H4MIDI WC
**Master clock:** KeyStep Pro
**Configuration software:** HxMIDI Tools

---

## Instrument Inventory

| Instrument | Role | Connection to H4MIDI | MIDI Channel(s) |
|---|---|---|---|
| KeyStep Pro | Master clock + sequencer | USB Host 1 | source (all) |
| UC33e | CC controller (synths + mixer) | USB Host 2 | source (multi-ch) |
| nanoPad | Pads / sequence trigger | USB Host 3 | source (multi-ch) |
| U2MIDI Pro | USB→DIN adapter for XR18 | USB Host 4 | — (passthrough) |
| Zynthian | Slave synth | USB Host 5 | ch 9–11 |
| Axoloti | Slave synth | USB Host 6 | ch 6 |
| TD-3 | Slave synth / bass | USB Host 7 | ch 7 |
| MachineDrum | Slave drum machine | DIN OUT 1 | ch 1–4 |
| MicroKorg | Slave synth | DIN OUT 2 | ch 5 |
| XR18 | Slave mixer (CC) · audio USB → DAW | DIN IN via U2MIDI Pro | ch 8 |
| Millennium e-drums | Drum trigger → DAW only | USB direct to PC | — |

> **Millennium:** connected directly to the computer via USB, independent from the H4MIDI WC.
> Not part of the MIDI routing — listed here for setup completeness.

> **XR18:** USB port reserved for 18-channel multitrack audio to DAW.
> MIDI control arrives via U2MIDI Pro (USB Host 4) → DIN cable → XR18 physical MIDI IN.

> **KeyStep Pro THRU:** no dedicated THRU port. OUT 2 can be reconfigured as THRU via
> Arturia MIDI Control Center, but is then no longer usable as a second MIDI OUT simultaneously.

---

## H4MIDI WC Physical Ports

| Port | Device | Direction | Notes |
|---|---|---|---|
| USB-A Host 1 | KeyStep Pro | IN | Master clock + note/seq source |
| USB-A Host 2 | UC33e | IN | CC control source. Has DIN IN/OUT but used via USB here. |
| USB-A Host 3 | nanoPad | IN | Note / pad trigger source. USB only device. |
| USB-A Host 4 | U2MIDI Pro | IN+OUT | Adapter → DIN cable → XR18 MIDI IN |
| USB-A Host 5 | Zynthian | OUT | Slave — enable USB gadget mode in Zynthian OS |
| USB-A Host 6 | Axoloti | OUT | Slave ch 6. micro-USB device port. |
| USB-A Host 7 | TD-3 | OUT | Slave ch 7. USB type-B. |
| USB-A Host 8 | — | — | Free |
| DIN OUT 1 | MachineDrum IN | OUT | Ch 1–4 + clock |
| DIN OUT 2 | MicroKorg IN | OUT | Ch 5 + clock |
| DIN IN 1 | MachineDrum OUT | IN | Optional return → DAW |
| DIN IN 2 | MicroKorg OUT | IN | Optional return → DAW |
| USB-C Client | Computer / DAW | IN+OUT | HxMIDI Tools + 4 virtual MIDI ports |

---

## Routing Matrix — HxMIDI Tools › Router tab

Select an input (turns orange) → check each output it should feed.
All changes are saved automatically to the device.

### Input: KeyStep Pro (USB Host 1)
Sends: notes, sequences, MIDI clock (24 PPQN)

| Output | Device | Enabled |
|---|---|---|
| DIN OUT 1 | MachineDrum | ✅ |
| DIN OUT 2 | MicroKorg | ✅ |
| USB Host 4 out | U2MIDI Pro → XR18 | ✅ |
| USB Host 5 out | Zynthian | ✅ |
| USB Host 6 out | Axoloti | ✅ |
| USB Host 7 out | TD-3 | ✅ |
| USB Host 2 out | UC33e | ❌ loop |
| USB Host 3 out | nanoPad | ❌ loop |

---

### Input: nanoPad (USB Host 3)
Sends: notes, pad triggers, sequences

| Output | Device | Enabled |
|---|---|---|
| DIN OUT 1 | MachineDrum | ✅ |
| DIN OUT 2 | MicroKorg | ✅ |
| USB Host 4 out | U2MIDI Pro → XR18 | ⚠️ only if triggering XR18 scenes from pads |
| USB Host 5 out | Zynthian | ✅ |
| USB Host 6 out | Axoloti | ✅ |
| USB Host 7 out | TD-3 | ✅ |
| USB Host 1 out | KeyStep Pro | ❌ loop |
| USB Host 2 out | UC33e | ❌ loop |

---

### Input: UC33e (USB Host 2)
Sends: CC messages for parameter and volume control

| Output | Device | Enabled |
|---|---|---|
| DIN OUT 1 | MachineDrum | ✅ |
| DIN OUT 2 | MicroKorg | ✅ |
| USB Host 4 out | U2MIDI Pro → XR18 | ✅ |
| USB Host 5 out | Zynthian | ✅ |
| USB Host 6 out | Axoloti | ✅ |
| USB Host 7 out | TD-3 | ✅ |
| USB Host 1 out | KeyStep Pro | ❌ |
| USB Host 3 out | nanoPad | ❌ |

---

### Input: DIN IN 1 — MachineDrum OUT (optional)

| Output | Device | Enabled |
|---|---|---|
| USB-C Client port 1 | DAW | ✅ if recording MD output |
| everything else | — | ❌ |

---

### Input: DIN IN 2 — MicroKorg OUT (optional)

| Output | Device | Enabled |
|---|---|---|
| USB-C Client port 2 | DAW | ✅ if recording MK output |
| everything else | — | ❌ |

---

## Filter Table — HxMIDI Tools › Filter tab

Select the output from the dropdown → orange = blocked, grey = passes through.
Configure each output port separately.

| Output | Device | Channels that pass | Blocked channels | Blocked message types |
|---|---|---|---|---|
| DIN OUT 1 | MachineDrum | ch 1, 2, 3, 4 | ch 5–16 | none |
| DIN OUT 2 | MicroKorg | ch 5 | ch 1–4, 6–16 | none |
| USB Host 4 out | U2MIDI → XR18 | ch 8 | ch 1–7, 9–16 | Note On, Note Off, Clock, Sysex |
| USB Host 5 out | Zynthian | ch 9, 10, 11 | ch 1–8, 12–16 | none |
| USB Host 6 out | Axoloti | ch 6 | ch 1–5, 7–16 | none |
| USB Host 7 out | TD-3 | ch 7 | ch 1–6, 8–16 | none |

### XR18 message filter detail

| Message type | To XR18 | Reason |
|---|---|---|
| Ctrl Change (CC) | ✅ passes | Controls faders, sends, EQ |
| Note On / Note Off | ❌ blocked | Prevents accidental scene/mute triggers |
| Clock / Timing | ❌ blocked | Mixer does not need sync |
| Program Change | ⚠️ optional | Only if using XR18 scenes via PC |
| Sysex | ❌ blocked | Not required |

---

## MIDI Clock Distribution

Clock (24 PPQN) travels within the same MIDI stream as note data.
No separate routing needed — enabling an output in the Router is sufficient.

| Device | Receives clock | Internal setting required |
|---|---|---|
| MachineDrum | ✅ via DIN OUT 1 | Global → Clock Source → External MIDI |
| MicroKorg | ✅ via DIN OUT 2 | Global → MIDI Clock → External |
| TD-3 | ✅ via USB Host 7 | Settings → MIDI Clock → External (or USB) |
| Axoloti | ✅ via USB Host 6 | Patch: add `midi/in/timingclock` object |
| Zynthian | ✅ via USB Host 5 | Menu → MIDI → Clock Source → External |
| XR18 | ❌ blocked via Filter | Not required |

---

*Setup: CME H4MIDI WC + CME U2MIDI Pro · Configured via HxMIDI Tools*
*Specifications verified against official manufacturer sources.*
