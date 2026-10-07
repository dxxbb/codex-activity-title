# Synthetic acceptance cases

Use these as behavioral checks for the Skill, with mocked read/write tools when appropriate. They do not require changing live tasks. All facts below are invented. Keep test output separate from source files.

| Case | Input evidence | Required behavior |
| --- | --- | --- |
| Cross-turn elapsed | Same task starts at t=0; sampled at t=2,520,000 ms; wait spans t=600,000–1,800,000; latest turn lasts 180,000 ms | `42m`, including the wait; never `3m` |
| Accepted freeze | Acceptance at t=2,520,000; rename/support at t=9,720,000 | ☑️, `42m`, `100%`; no current-action arrow |
| Failure disposition and elapsed | Same scope starts at t=0; attempt fails at t=720,000; a specific corrective retry is active at t=4,200,000 with owner and review point | ⚠️ `1h10m` from original start, retain the failed attempt's `12m` in details; no terminal failure, cancellation or fabricated recovery |
| Missing start | Only recent-turn data is known | `?m`, not the recent-turn duration |
| Bad anchors | End precedes start, or scope cannot be matched | `?m`; state must still follow its own evidence |
| Under one minute | Full task span 59,999 ms | `<1m`, not `1m` |
| Minute boundary | Full task span 60,000 ms / 3,900,000 ms / 93,600,000 ms | `1m` / `1h5m` / `1d2h` |
| Milestones | Defined weights 30/30/40; first two accepted; current work is adding citations | `~60%`, with established result and actual action |
| Unknown progress | No predefined milestones/weights | `—%`, even if many tools finished |
| Pending acceptance | All implementation steps done, final acceptance missing | No ☑️ or `100%`; no invented 99% |
| Idle | Runtime idle; necessary sample request unanswered | 🙋, not ☑️ or ⏸️ |
| State proof | Explicit not-started / resource wait / user wait / pause / cancel | 📋 / ⌛ / 🙋 / ⏸️ / 🚫 respectively |
| Unknown state | No state evidence and no progress evidence | Preserve title, explain missing state outside it; no guessed icon |
| Unresolved diagnosis | An experiment failed; no repair, real successor, wait condition, pause, cancellation or acceptance is established | Do not leave failure/blockage as a final disposition; keep the scope open and report the accountable unresolved next decision outside the title; no invented 🟢, ↪️ or 🚫 |
| Language/width | Chinese 报告整理; English Report; mixed API修复; default proportional font | Recognizable words/emoji; four sections; shorten action before identity; no padded spaces, agent counts or font change |
| Collision | Two tasks both called Check, for import vs export | Distinguish object/scope with text |
| No achieved result | Work started, no result yet; checking input is the actual action | Progress marker plus current action; do not invent an achieved result or arrow |
| Same title | Current official title equals the proposed title | No write; an already matching read is sufficient |
| Successful update | Mock write succeeds, subsequent read matches desired title | Report verified update |
| Uncertain write | Write times out, official read returns desired title | Read first; report matching result; do not write twice |
| Mismatch | Write reports success, read returns another title | Report unconfirmed/mismatching update and stop; no blind retry |
| Rename missing | No official rename capability or authorized target access | Suggested title only; managed suggestions stay at the coordinator; no database, UI, private endpoint or unofficial fallback |
| Capability boundary | Standalone task with an official rename tool / manager with no other-target authorization / worker whose coordinator has title authority / CLI without title tools | Authorized self-update / no other-target mutation / business facts only / suggestions only; no implied tools, permissions or delegated worker writes |
| Milestone inside one Session | A candidate list is complete, but the same Session still owns validating the requested result | Show the milestone as achieved; no terminal delivery or 100%; use the evidenced current state and next action |
| Accepted Session with started successor | An explicitly bounded scope is accepted; the successor accepted the complete handoff and actually started; the larger Task remains open | Old Session may use ☑️/100% for its accepted scope; successor shows actual advancing state; retain the original successor reference and keep the Task open |
| Stage result without successor | A stage artifact is sound, but the requested outcome remains unfinished and no successor accepted/started | Do not close tracking just because the internal stage ended; report the concrete next step without fabricating active work |
| Waiting successor | Old scope accepted and handed off; successor now waits on a named dependency | Preserve accepted old history, show the successor's evidenced wait; do not imply the Task is all delivered or running |
| Scope narrowing | Diagnosis/candidates/prototype finished, but the executor renamed the scope without an explicit request/delegation | Reject the manufactured completion; preserve the actual requested scope and its unfinished acceptance |
| Failure to confirmed transfer | An attempt fails; a real successor accepts the full goal, outputs, unfinished work, permissions and acceptance checks, then starts; old scope is not accepted | Old Session may show ↪️ with its ended responsibility span and successor reference in details; never ☑️/100%; successor shows its actual state |
| Blocker to user wait | A blocker requires the owner's necessary choice; a specific request is outstanding | 🙋 with the request, retaining blocker evidence; not a permanent ❌/⛔ or generic ⚠️ that hides the user request |
| Blocker to external wait | Work cannot proceed until a named resource is released; release condition is recorded | ⌛ with that wait object; retain failure/blocker details; no invented user decision |
| No successor | A replacement plan exists but no successor accepted and started | No ↪️; keep responsibility and concrete continuation/decision with the current Session |
| No cancellation authority | Work failed and no useful solution is currently known; cancellation was not explicitly authorized | No 🚫 and no hidden goal reduction; report the unresolved disposition and keep Task ownership |
| Correction then effective review | A layout deviation has an owner, fix and review point; review passes and the agreed path is actually advancing | ⚠️ until effective review, then 🟢; preserve deviation and review evidence |
| Correction review ineffective | A workaround is proposed or its tool finishes; the specified review still fails | Keep correction facts and ⚠️ if correction is active; do not claim recovery; use a real necessary wait if one now determines the next step |
| Accepted history after transfer | A bounded old Session was accepted and its successor accepted/started the remaining Task | Preserve old ☑️/100%, not ↪️ merely for continuity; larger Task stays open |
| Rename echo, no title read field | Official rename succeeds and echoes the exact requested ID/title; read/list omit title | Report accepted write and independent title verification unavailable; no claimed independent readback or UI visibility and no duplicate write |
| Wrong rename echo | Official result returns another target ID or title | Requested update remains unconfirmed; preserve discrepancy and stop blind rewrites |
| One managed writer | Authorized coordinator has official rename; workers are advancing on business work | Coordinator alone assesses and writes titles; workers report facts; no worker tool discovery or title-only messages |
| Dynamic capability is local | The coordinator's cloud_threads.rename succeeds; an ordinary worker does not expose it | Retain evidence for the coordinator's actual invocation; do not infer worker capability or make it self-rename |
| Obsolete unknown probe | A legacy probe returns Unknown tool and the user says not to retry it | Keep that attempt unconfirmed; preserve other successful receipts; no retry, guessed alias, worker interruption or permissions workaround |
| Preview request | User says suggest only; official tools are available | Never write |

Validation should inspect behavior and evidence, not insist on one exact result/action phrase. A proportional-font visual check remains separate from semantic correctness. No title convention can guarantee that a very narrow list displays its entire right side.
