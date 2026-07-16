# Studio MIDI — Capabilities Reference

*All specifications verified against official sources and datasheets.*

---

## MIDI Capabilities per Instrument

| Instrument | MIDI IN | MIDI OUT | MIDI THRU | DIN 5-pin | USB MIDI | Notes |
|---|---|---|---|---|---|---|
| KeyStep Pro | ✅ | ✅ | ⚠️ | ✅ | ✅ | 1× DIN IN, 2× DIN OUT. No dedicated THRU port — OUT 2 can be reconfigured as THRU via MIDI Control Center software (not simultaneously usable as OUT). |
| UC33e (Evolution) | ✅ | ✅ | ❌ | ✅ | ✅ | DIN IN + DIN OUT physical ports. Not a THRU device per manual: DIN IN data cannot pass to DIN OUT without a computer in the chain. |
| nanoPad (Korg) | ✅ | ✅ | ❌ | ❌ | ✅ | USB only (mini-B). No DIN ports, no THRU. Internal routing via Korg Kontrol Editor software only. |
| MachineDrum (Elektron) | ✅ | ✅ | ✅ | ✅ | ❌ | Full DIN IN / OUT / THRU. No USB MIDI. |
| MicroKorg (Korg) | ✅ | ✅ | ✅ | ✅ | ❌ | Full DIN IN / OUT / THRU. No USB MIDI. |
| Zynthian | ✅ | ✅ | ❌ | ❌ | ✅ | USB only. Requires USB gadget mode in Zynthian OS to act as USB MIDI slave. No DIN ports on board. |
| Axoloti | ✅ | ✅ | ❌ | ✅ | ✅ | DIN IN + DIN OUT (5-pin). micro-USB device (class-compliant). USB-A host port. No hardware THRU — must be implemented in patch via `midi/in` + `midi/out` objects. |
| TD-3 (Behringer) | ✅ | ✅ | ✅ | ✅ | ✅ | DIN IN + combined DIN OUT/THRU (single shared port). USB type-B. DIN IN data echoed to DIN OUT. USB IN data copied to DIN OUT only. |
| XR18 (Behringer) | ✅ | ✅ | ❌ | ✅ | ✅ | DIN IN + DIN OUT. USB type-B for 18-ch multitrack audio + 16ch MIDI on same cable. No THRU. In this setup: MIDI control via DIN (through U2MIDI Pro adapter), USB dedicated to multitrack audio → DAW. |
| Millennium e-drums | ❌ | ✅ | ❌ | ❌ | ✅ | USB only. Trigger output direct to PC. Not part of H4MIDI WC routing. |
| U2MIDI Pro (CME) | — | — | — | ✅ | ✅ | Adapter only: USB ↔ DIN 5-pin passthrough. Used as USB Host 4 → DIN cable → XR18 MIDI IN. |

---

## MIDI Channel Map

| Ch | Instrument | Role |
|---|---|---|
| 1 | MachineDrum — part 1 | Drum / percussion voice 1 |
| 2 | MachineDrum — part 2 | Drum / percussion voice 2 |
| 3 | MachineDrum — part 3 | Drum / percussion voice 3 |
| 4 | MachineDrum — part 4 | Drum / percussion voice 4 |
| 5 | MicroKorg | Synth / bass / lead |
| 6 | Axoloti | DSP synth / effects |
| 7 | TD-3 | Bass line / acid |
| 8 | XR18 | Mixer CC control (faders, sends, EQ) |
| 9 | Zynthian — part 1 | Synth voice 1 |
| 10 | Zynthian — part 2 | Synth voice 2 |
| 11 | Zynthian — part 3 | Synth voice 3 |
| 12 | — | Free |
| 13 | — | Free |
| 14 | — | Free |
| 15 | — | Free |
| 16 | — | Free |

> Ch 1–4 all routed to MachineDrum — each part responds on its own channel.
> Ch 12–16 free for future expansion.
> Millennium e-drums have no channel assignment in this setup (DAW-direct, USB only).

---

*Specifications verified against: Arturia official docs, Elektron support, Korg official specs,*
*Behringer wiki/manuals, Axoloti official site and community docs.*
*Studio MIDI Reference · CME H4MIDI WC · HxMIDI Tools*
