# RDAC Roland's proprietary sample format inside the BOSS SP-202, BOSS SP-303 and Roland SP-555 Samplers

The BOSS Dr. Sample SP-202, SP-303 and the Roland SP-555, legendary portable hardware samplers, store their samples internally and on memory cards in **RDAC**[^1], Roland's own proprietary audio compression format. Roland never documented it. For the SP-202 and SP-303 there was never any computer software for it at all: the only way audio ever got onto a card was through the machine itself. The SP-555 had the SP-555 WAV Converter, long since abandoned.

Which means that for decades, everything on those cards — your samples, your sets, whole eras of beat-making — could only be read by the samplers themselves, or, for the SP-555, by that one aging utility.

Now, RDAC for the SP-303 and SP-555 has been fully reverse-engineered: reading and writing, in every quality mode. And the SP-202 — long the most inaccessible of the three — is partially understood: its samples already decode perfectly.

## The machines

| Sampler | Card | Sample modes |
|---|---|---|
|   BOSS Dr. Sample SP-202 (1998)   | 5V SmartMedia |  HI-FI, STANDARD, LO-FI 1, LO-FI 2  |
| BOSS Dr. Sample SP-303 (2001) | 3V SmartMedia | STANDARD, LONG, LO-FI |
| Roland SP-555 (2008) | CompactFlash | STANDARD, LO-FI |

*The Boss Dr. Sample SP-202 (1998) uses 5V SmartMedia cards that almost no modern reader can touch — and worse, some readers that do accept one can silently damage it just by reading it, so an original SP-202 card should never go into a generic card reader. A card image has now been safely captured with a Fujifilm SM-R1, and it turns out the SP-202 speaks the same RDAC dialect as the SP-303's LO-FI mode: even its top HI-FI grade is that same codec, just run at a higher sample rate. Its samples already decode perfectly with the solved codec; writing back isn't byte-exact yet, because the SP-202's own encoder makes slightly different choices along the way. Limited SP-202 support is planned for Dr. Sidekick.*

## What RDAC actually is

RDAC is a clever space-saver. Instead of storing every detail of the sound, it stores a running *prediction* of where the audio is headed plus small corrections to keep it on track — a bit like writing down directions as "keep going straight, nudge left" instead of listing every coordinate. That's how these machines squeezed respectable sampling time out of the tiny memory cards of their day: STANDARD mode fits audio into roughly half the space of a CD-quality recording, and the LONG and LO-FI modes trade fidelity for even more time. It's also exactly why nothing standard could ever read the files — the "directions" only make sense if you know Roland's rules for following them.

## How it was cracked

Patiently, with real hardware on the desk. Known test signals were sampled onto real cards and the resulting bytes picked apart until the patterns gave themselves up. Hunches were tested in the most honest way possible: write a file back to a card, put it in the sampler, press the pad, and listen. The firmware inside the machines was studied to settle the questions the cards alone couldn't answer. For the SP-303 this was done completely from scratch — with no software to compare against, the machine's own recordings were the only teacher.

## Does it really work?

Yes — and not just "sounds right." The reverse-engineered encoder produces files **byte-for-byte identical** to what the hardware itself records, verified across tens of thousands of test blocks in every mode on the SP-303 and SP-555. Cards authored this way have been loaded and played on the real samplers. As far as an SP-303 or SP-555 is concerned, these files came from home.

For the SP-202 the story is, so far, read-only: decoding an entire card back to audio works with zero errors, but re-encoded audio doesn't yet match the machine's own bytes exactly — it differs only in the last few least-significant bits, and closing that gap is ongoing work.

## The fine print

This work was done independently, for interoperability — so people can keep using instruments they own and recover audio they made. The SP-303 format was solved purely from the hardware's own output; the SP-555 work was verified against the output of Roland's converter; the SP-202 findings come from studying an image of an original card. No Roland code or firmware is included or required. This project is not affiliated with or endorsed by Roland or BOSS.

## So how do I get at my samples?

With **[Dr. Sidekick](https://github.com/OneCoinOnePlay/Dr.Sidekick)** — a library manager for the SP-303 and SP-555 that reads and writes cards directly. Pull your old samples off a card as WAVs, or build a fresh card from WAVs on your computer, no vintage Windows software and no pad-by-pad resampling required.

And you don't need the sampler anymore — or even the card. If all that survives is a folder of card files copied onto a hard drive years ago, Dr. Sidekick can open those too and give you your audio back.

---

© 2026 One Coin One Play, licensed [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) — share and adapt freely with credit.

[^1]: RDAC stands for **Roland Digital Audio Coding**, and the SP samplers weren't its only home. Roland built RDAC lossy compression into its VS-series digital multitrack recorders (VS-880, VSR-880) and AR-series solid-state audio recorders (AR-3000R, AR-200S), where selectable RDAC modes and grades traded sound quality against recording time — a prized trick in the days of small, expensive SCSI drives and early memory cards. See [Roland's AR-series overview](https://proav.roland.com/global/articles/ar_series_overview/ar_series_recording_modes_times/). This page documents the variant the SP samplers write to their memory cards.
