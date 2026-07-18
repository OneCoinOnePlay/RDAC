# RDAC Roland's proprietary sample format inside the BOSS SP-303 and Roland SP-555 Samplers

The BOSS Dr. Sample SP-303 and the Roland SP-555, two legendary portable hardware samplers, store their samples internally and on memory cards in **RDAC**[^1], Roland's own proprietary audio compression format. Roland never documented it. For the SP-303 there was never any computer software for it at all: the only way audio ever got onto a card was through the machine itself. The SP-555 had the SP-555 WAV Converter, long since abandoned.

Which means that for decades, everything on those cards — your samples, your sets, whole eras of beat-making — could only be read by the samplers themselves, or, for the SP-555, by that one aging utility.

Now, RDAC for these two samplers has been fully reverse-engineered: reading and writing, in every quality mode.

## The machines

| Sampler | Card | Sample modes |
|---|---|---|
| BOSS SP-303 Dr. Sample (2001) | SmartMedia | STANDARD, LONG, LO-FI |
| Roland SP-555 (2008) | CompactFlash | STANDARD, LO-FI |

*Difficultly reading the *Boss Dr. Sample SP-202's (1998)* 5V SmartMedia cards means that one's going to have to wait to be cracked. I had limited success using a Fujifilm SM-R1.*

## What RDAC actually is

RDAC is a clever space-saver. Instead of storing every detail of the sound, it stores a running *prediction* of where the audio is headed plus small corrections to keep it on track — a bit like writing down directions as "keep going straight, nudge left" instead of listing every coordinate. That's how these machines squeezed respectable sampling time out of the tiny memory cards of their day: STANDARD mode fits audio into roughly half the space of a CD-quality recording, and the LONG and LO-FI modes trade fidelity for even more time. It's also exactly why nothing standard could ever read the files — the "directions" only make sense if you know Roland's rules for following them.

## How it was cracked

Patiently, with real hardware on the desk. Known test signals were sampled onto real cards and the resulting bytes picked apart until the patterns gave themselves up. Hunches were tested in the most honest way possible: write a file back to a card, put it in the sampler, press the pad, and listen. The firmware inside the machines was studied to settle the questions the cards alone couldn't answer. For the SP-303 this was done completely from scratch — with no software to compare against, the machine's own recordings were the only teacher.

## Does it really work?

Yes — and not just "sounds right." The reverse-engineered encoder produces files **byte-for-byte identical** to what the hardware itself records, verified across tens of thousands of test blocks in every mode on both machines. Cards authored this way have been loaded and played on the real samplers. As far as an SP-303 or SP-555 is concerned, these files came from home.

## The fine print

This work was done independently, for interoperability — so people can keep using instruments they own and recover audio they made. The SP-303 format was solved purely from the hardware's own output; the SP-555 work was verified against the output of Roland's converter. No Roland code or firmware is included or required. This project is not affiliated with or endorsed by Roland or BOSS.

## So how do I get at my samples?

With **[Dr. Sidekick](https://github.com/OneCoinOnePlay/Dr.Sidekick)** — a library manager for the SP-303 and SP-555 that reads and writes cards directly. Pull your old samples off a card as WAVs, or build a fresh card from WAVs on your computer, no vintage Windows software and no pad-by-pad resampling required.

And you don't need the sampler anymore — or even the card. If all that survives is a folder of card files copied onto a hard drive years ago, Dr. Sidekick can open those too and give you your audio back.

---

© 2026 One Coin One Play, licensed [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) — share and adapt freely with credit.

[^1]: RDAC stands for **Roland Digital Audio Coding**, and the SP samplers weren't its only home. Roland built RDAC lossy compression into its VS-series digital multitrack recorders (VS-880, VSR-880) and AR-series solid-state audio recorders (AR-3000R, AR-200S), where selectable RDAC modes and grades traded sound quality against recording time — a prized trick in the days of small, expensive SCSI drives and early memory cards. See [Roland's AR-series overview](https://proav.roland.com/global/articles/ar_series_overview/ar_series_recording_modes_times/). This page documents the variant the SP-303 and SP-555 write to their memory cards.
