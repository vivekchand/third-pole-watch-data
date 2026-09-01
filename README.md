# Third Pole Watch — Data & Audit Trail

This repository is the **tape** that the [Third Pole Watch](https://github.com/vivekchand/third-pole-watch)
seismic monitor writes: every few minutes the watch daemon commits its current
state here, so the full history of what the watch claimed — and when — is
public, permanent, and tamper-evident. Nothing here is written by humans.

Live view: **https://thirdpole.watch**

## Files

| File | What it is | Cadence |
|---|---|---|
| `status.json` | Ledger score (days running, candidates, verdicts) + `generated_at` heartbeat | every ~5 min, and immediately on any candidate |
| `live.json` | Downsampled waveform envelopes (last 10 min per station) that the site renders | with every publish |
| `ledger.jsonl` | Append-only candidate log with human verdicts — the false-alarm record | with every publish |

## Why a public audit trail

No detector should ever feed real alerting without a measured false-alarm
record. Because each publish is a git commit, this history cannot be quietly
edited: every candidate, every false alarm, every gap in the heartbeat is in
the log forever. `git log -p status.json` replays the watch's entire life.

Future datasets (backstop scan results, station inventories, InSAR watch
lists) will live here too, so they can be diffed and compared in one place.

*The watch is a research instrument, not an official warning service.
Official alerts come from national authorities.*
