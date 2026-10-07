---
name: activity-title
description: Generate and update compact Codex Activity titles that show task status, identity, elapsed time, and evidence-based progress. Use when asked to maintain task titles or make the Activity list easier to scan; give a suggestion when official title tools are unavailable.
---

# Activity Title

Version: 0.1.

Turn the title of the requested task into a truthful, compact status line. Use the language the user explicitly requests, otherwise the current task's conversation language. English installation examples and these instructions do not force English titles. Apply this convention only to the task(s) they requested. A suggestion-only request must not write a title.

```text
status │ project icon + short task │ elapsed │ progress + achieved → current action
```

Keep four sections with ` │ ` between them, including the separator immediately after status. Status is an icon alone. Do not add agent counts or pad spaces to align columns. Use the existing default proportional font; do not install or change fonts.

## Scope and status

Distinguish the user's **Task** (requested outcome and acceptance) from a **Session** (an execution context with a concrete scope). This title represents the requested Session. Bind its scope to the user's request or an explicit, traceable delegation; do not silently narrow an unfinished goal into a diagnosis, candidate list or prototype to manufacture completion. Use business-acceptance and Task → current Session evidence supplied by the task owner/coordinator, or the current Session's explicit request and records. This Skill displays those evidenced facts and does not redefine the user's goal.

Prefer continuing the same work chain in the same Session. A milestone alone is an achieved fact, not a terminal event. An independently accepted Session scope may end while the larger Task stays open only when the unfinished work has a traceable successor that has actually accepted the handoff and started. Read the recorded acceptance and successor evidence; coordination owns the handoff and Task tracking. Do not create a new Session merely to change a title. An active successor may later wait or become blocked; do not mark the whole Task delivered or fabricate running work. Without a successor, preserve unfinished tracking and a concrete next step. Do not undo valid accepted Session history merely because its larger Task remains open.

Preserve the evidenced Session scope across turns, waits and renames. A retry within the same unfinished scope keeps its first start. A genuinely new scope must not extend the completed original scope's elapsed time.

Choose a state only when its evidence is present:

| Icon | Enter when | Leave when |
| --- | --- | --- |
| 📋 | The task is explicitly not started | Work begins |
| 🔵 | Work is actually advancing on the agreed path | A correction or another evidenced state applies |
| ⚠️ | A concrete deviation needs or is undergoing correction; record its owner, corrective action and review point | Effective review confirms the correction; use the actual resulting state, or a specific wait/pause/transfer decision |
| ↪️ | Responsibility has moved to a real successor that accepted the complete handoff and actually started; retain its reference | Follow any newly evidenced responsibility change; this is not delivery acceptance |
| ⌛ | A named dependency/resource is pending, with a release condition | The dependency clears |
| 🙋 | A necessary request awaits the user's response | The response allows work to continue |
| ⏸️ | There is an explicit pause decision | Work resumes or is cancelled |
| ✅ | The named deliverable meets its acceptance criteria | A new scope is established; do not undo accepted history for unrelated follow-up |
| 🚫 | There is an explicit cancellation decision | A new scope is explicitly restarted |

When evidence conflicts, use the fact that currently determines the next step. Runtime `idle`, a finished tool call, or a final assistant message is not proof of acceptance, pause, failure, or cancellation. If the state is unknown, do not invent a fallback icon: preserve the current title and explain the missing state evidence outside it. Do not add other states without agreeing on their meaning and entry/exit conditions.

Failure (❌) and blockage (⛔) are temporary diagnoses, not lasting terminal dispositions. Preserve the failed attempt and blocker in the original Session evidence, then display the evidenced next disposition: authorized execution, correction, confirmed transfer, a necessary user/external wait, explicit pause/cancellation, or accepted delivery. The task owner/coordinator must resolve an undecided disposition; this title Skill must not fabricate recovery, invent a wait or silently cancel the user's Task. A temporarily preserved old diagnostic title is stale/unconfirmed: proactively explain the pending owner disposition outside it, then update on the established disposition event; do not leave it as the current final status. Active diagnosis can be correction only with a specific deviation, responsible owner, corrective action and review point. ⚠️ does not itself mean the user must intervene: a necessary user response uses 🙋 and a named external release condition uses ⌛. Do not restore 🔵 merely because a workaround was proposed or a tool ended; first verify the correction and the actual current state.

Use ↪️ for confirmed transfer of unresolved responsibility, not a planned handoff or an unstarted successor. An independently accepted old Session keeps ✅ and its accepted history rather than changing to ↪️ merely because the larger Task continues. Keep the successor reference outside the compact title; do not claim 100% for transfer.

## Elapsed time and progress

Use trustworthy anchors for this Session scope's first start and latest sampled event. Elapsed time includes waiting. Thread creation time or a last-turn duration is not the scope's start unless evidence establishes that they cover exactly the named scope. If only recent-turn data is available, show `?m`. For a confirmed single-turn scope, precise duration data may establish that full span.

Freeze elapsed time when this Session's responsibility actually ends through scoped acceptance, a confirmed transfer, or explicit cancellation. Failure/blockage diagnosis does not end an unresolved scope or freeze its elapsed time; correction, retries and waits in that same scope retain its original start. Preserve a failed attempt's own duration separately in its evidence. Later support, opening an artifact, or renaming must not increase a genuinely ended scope's elapsed time. Missing, reversed, or ambiguous anchors produce `?m`, not `0m`.

Format known elapsed time by flooring, never rounding up: below one minute `<1m`; below one hour `18m`; below one day `1h5m` (omit zero minutes); one day or more `1d2h` (omit zero hours). Keep full anchors in the task evidence so this compact display can be recomputed; it is not a live timer.

Progress comes from predefined acceptance milestones and their weights, not elapsed time, tokens, agent counts or test pass ratios. Sum the accepted milestones to form a defensible estimate, displayed as `~N%` from 0–99. If milestones/weights are unknown, show `—%`. Do not invent weights after the fact. When everything looks complete but acceptance is pending, retain a defensible estimate below 100 or use `—%`; never imply acceptance with an arbitrary 99. Only an accepted named deliverable uses `100%` with ✅.

In the final section, put an established result before `→` and the actual current action or wait object after it. With no established result, omit that part and the arrow. With no current action, omit the arrow. Accepted, transferred and cancelled Sessions omit a current-action arrow; describe the scoped outcome. Other states show the actual next action or wait object when known. Do not create a result just to fill the field.

## Identity and narrow width

Use a stable, recognizable short task name plus one helpful project/type icon. Text must identify the task without the icon. For collisions, include a meaningful object or scope distinction. Avoid changing the task name every time the action changes.

Budget a short name at roughly 4–5 Chinese characters' visual width; English uses proportional glyph widths, not a four-letter limit. Prefer a complete word or recognizable abbreviation. For narrower displays, shorten the result/action phrase first, then the task name while retaining its identity. Keep status, the first separator, time/unknown markers, and all four sections. If the fourth section must become very short, retain the progress marker. Do not cut an emoji sequence, half a Chinese phrase, or an English word into meaningless fragments. A UI may still truncate the right side; do not claim fixed columns or guaranteed visibility. When measurement is unavailable, describe width as approximate.

Synthetic examples:

```text
🔵 │ 📄报告整理 │ 18m │ ~60%提纲已定→补引用
🙋 │ 🧪Check │ 42m │ —%need sample
✅ │ 🔧Export │ 12m │ 100%verified
⚠️ │ 🧩布局检查 │ 4m │ —%偏差已查→修布局
↪️ │ 🧪功能验证 │ 12m │ —%已转交
```

## Standalone and managed ownership

For an ordinary standalone task, the requested agent may maintain its own title when its runtime exposes an official rename tool and confirms the requested target. A dot or manager context is not required. Installing this Skill does not provide those tools or authorize other-target writes.

For a managed group, the active authorized coordinator alone judges the business facts, constructs titles, writes them and verifies the available evidence. Workers report their current work, outputs, waits, timing anchors and acceptance facts; they do not discover title tools or rename themselves. Do not send title-only messages that interrupt business execution. A worker's available tools do not transfer title-writing authority. Missing coordinator capabilities are reported by the coordinator rather than distributed to workers. A management handoff requires explicit authorization and confirmed takeover so there is still one writer.

## Event updates and official tools

Update when this agent handles a meaningful event: start, milestone, waiting/clearance, pause/resume, failure/blocker diagnosis and its disposition, correction/review, confirmed transfer, cancellation, or acceptance. Do not invent a background watcher or promise refreshes while the agent is idle. Avoid polling solely to advance the time field.

Tool availability belongs to the current runtime and invocation, not to the Skill or a session label. Discover the actual official surface and follow its current schema. Examples include `mcp__codex_app__set_thread_title` and the dynamically exposed `cloud_threads.rename`; their presence must be established in the writing agent's current runtime. An observed coordinator's successful rename is not proof that ordinary sessions or workers expose that tool. Other-target writes require explicit authorization for the named targets and official access to them.

1. Resolve the requested target from trusted runtime context or official discovery, and confirm the exact identity through the available official target metadata. Build the desired title from evidenced business facts and the latest applicable user-approved convention. Read the existing title when the host exposes it; if it already matches, skip the write. A read/list response with no title field cannot establish equality.
2. Use the currently exposed official rename tool and its real argument schema. A documented current-target default may be used for an authorized self-update; other-target updates use their confirmed identity and backing kind when required. Preserve the actual result. A successful official result establishes an accepted write according to that tool's schema; if it echoes an ID and title, both must match the requested target and desired title. A mismatch, missing success or uncertain outcome stays unconfirmed.
3. Independently read the same target's title when an official read/list field is available. A matching value verifies that readback. If those tools omit a title field, report the accepted-write receipt and independent title verification as unavailable. A write response echo is not an independent readback, and neither establishes what the user has seen. Do not repeat a successful write merely because independent verification is unavailable. If an available readback disagrees, retain the disagreement and stop blind rewrites; if the write outcome is uncertain, read before considering another write.

If the official rename capability or authorized target access is missing, give a suggested title and report the missing capability. Keep managed-group suggestions at the coordinator. A missing independent title-read field is a verification gap, not proof that a successful official write failed. Honor an instruction not to retry an obsolete probe returning `Unknown tool`; do not cycle guessed aliases or make workers recover it. Do not edit a database, use UI automation, call private endpoints or substitute an unofficial command to bypass missing title tools. Never claim a suggestion was applied or a background refresh was implemented.

For behavioral review or changes to this convention, use [acceptance cases](references/acceptance-cases.md). The examples are synthetic; public examples and demonstrations must not contain private task names, timelines, paths, accounts, addresses, or thread identifiers.
