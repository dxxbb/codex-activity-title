# Synthetic acceptance cases

Use these as behavioral checks for the Skill, with mocked read/write tools when appropriate. They do not require changing live tasks. All facts below are invented. Keep test output separate from source files.

| Case | Input evidence | Required behavior |
| --- | --- | --- |
| Cross-turn elapsed | Same task starts at t=0; sampled at t=2,520,000 ms; wait spans t=600,000–1,800,000; latest turn lasts 180,000 ms | `42m`, including the wait; never `3m` |
| Accepted freeze | Acceptance at t=2,520,000; rename/support at t=9,720,000 | ✅, `42m`, `100%`; no current-action arrow |
| Failed freeze/retry | Same scope first starts at t=0; attempt ends at t=720,000; idle review at t=3,600,000; same-scope retry at t=4,200,000 | ❌ `12m` while ended; retry 🟢 `1h10m` from original start; do not mark the project failed |
| Missing start | Only recent-turn data is known | `?m`, not the recent-turn duration |
| Bad anchors | End precedes start, or scope cannot be matched | `?m`; state must still follow its own evidence |
| Under one minute | Full task span 59,999 ms | `<1m`, not `1m` |
| Minute boundary | Full task span 60,000 ms / 3,900,000 ms / 93,600,000 ms | `1m` / `1h5m` / `1d2h` |
| Milestones | Defined weights 30/30/40; first two accepted; current work is adding citations | `~60%`, with established result and actual action |
| Unknown progress | No predefined milestones/weights | `—%`, even if many tools finished |
| Pending acceptance | All implementation steps done, final acceptance missing | No ✅ or `100%`; no invented 99% |
| Idle | Runtime idle; necessary sample request unanswered | 🙋, not ✅ or ⏸️ |
| State proof | Explicit not-started / resource wait / user wait / pause / cancel | 📋 / ⌛ / 🙋 / ⏸️ / 🚫 respectively |
| Unknown state | No state evidence and no progress evidence | Preserve title, explain missing state outside it; no guessed icon |
| Failure | An experiment ended unsuccessfully, no active retry | ❌, not ⌛, ⛔ or 🚫 |
| Language/width | Chinese 报告整理; English Report; mixed API修复; default proportional font | Recognizable words/emoji; four sections; shorten action before identity; no padded spaces, agent counts or font change |
| Collision | Two tasks both called Check, for import vs export | Distinguish object/scope with text |
| No achieved result | Work started, no result yet; checking input is the actual action | Progress marker plus current action; do not invent an achieved result or arrow |
| Same title | Current official title equals the proposed title | No write; an already matching read is sufficient |
| Successful update | Mock write succeeds, subsequent read matches desired title | Report verified update |
| Uncertain write | Write times out, official read returns desired title | Read first; report matching result; do not write twice |
| Mismatch | Write reports success, read returns another title | Report unconfirmed/mismatching update and stop; no blind retry |
| Tools missing | No official read or write tool | Suggested title only; no database, UI, private endpoint or unofficial fallback |
| Capability boundary | Ordinary task with official tools / manager with no other-target authorization / CLI without title tools | Self-update allowed / no other-target mutation / suggestions only; no implied tools or permissions |
| Preview request | User says suggest only; official tools are available | Never write |

Validation should inspect behavior and evidence, not insist on one exact result/action phrase. A proportional-font visual check remains separate from semantic correctness. No title convention can guarantee that a very narrow list displays its entire right side.
