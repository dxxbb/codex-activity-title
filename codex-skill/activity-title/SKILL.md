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

Identify the concrete work named by the title and its acceptance criteria from the request and available task evidence. Preserve that scope across turns, waits and renames. A retry within the same scope keeps its first start. New follow-up work needs its own scope; it must not extend the completed original task's elapsed time.

Choose a state only when its evidence is present:

| Icon | Enter when | Leave when |
| --- | --- | --- |
| 📋 | The task is explicitly not started | Work begins |
| 🟢 | Work is actually advancing | Another evidenced state applies |
| ⌛ | A named dependency/resource is pending, with a release condition | The dependency clears |
| 🙋 | A necessary request awaits the user's response | The response allows work to continue |
| ⏸️ | There is an explicit pause decision | Work resumes or is cancelled |
| ✅ | The named deliverable meets its acceptance criteria | A new scope is established; do not undo accepted history for unrelated follow-up |
| ❌ | This attempt has ended unsuccessfully | A retry begins, or a new terminal decision applies |
| 🚫 | There is an explicit cancellation decision | A new scope is explicitly restarted |

When evidence conflicts, use the fact that currently determines the next step. Runtime `idle`, a finished tool call, or a final assistant message is not proof of acceptance, pause, failure, or cancellation. If the state is unknown, do not invent a fallback icon: preserve the current title and explain the missing state evidence outside it. Do not add ⛔ or any other state without first agreeing on its meaning and entry/exit conditions. Failure of one attempt is not failure of the whole project.

## Elapsed time and progress

Use trustworthy anchors for this task's first start and latest sampled event. Elapsed time includes waiting. Thread creation time or a last-turn duration is not the task start unless evidence establishes that they cover exactly the named scope. If only recent-turn data is available, show `?m`. For a confirmed single-turn task with matching scope, precise duration data may establish that full span.

Freeze elapsed time at the evidenced business end: acceptance, terminal failure of this attempt, or cancellation. Later support, opening an artifact, or renaming must not increase it. A retry of the same unfinished scope resumes elapsed time from its original start. Missing, reversed, or ambiguous anchors produce `?m`, not `0m`.

Format known elapsed time by flooring, never rounding up: below one minute `<1m`; below one hour `18m`; below one day `1h5m` (omit zero minutes); one day or more `1d2h` (omit zero hours). Keep full anchors in the task evidence so this compact display can be recomputed; it is not a live timer.

Progress comes from predefined acceptance milestones and their weights, not elapsed time, tokens, agent counts or test pass ratios. Sum the accepted milestones to form a defensible estimate, displayed as `~N%` from 0–99. If milestones/weights are unknown, show `—%`. Do not invent weights after the fact. When everything looks complete but acceptance is pending, retain a defensible estimate below 100 or use `—%`; never imply acceptance with an arbitrary 99. Only an accepted named deliverable uses `100%` with ✅.

In the final section, put an established result before `→` and the actual current action or wait object after it. With no established result, omit that part and the arrow. With no current action, omit the arrow. Terminal states omit the arrow/action; describe the actual outcome. Do not create a result just to fill the field.

## Identity and narrow width

Use a stable, recognizable short task name plus one helpful project/type icon. Text must identify the task without the icon. For collisions, include a meaningful object or scope distinction. Avoid changing the task name every time the action changes.

Budget a short name at roughly 4–5 Chinese characters' visual width; English uses proportional glyph widths, not a four-letter limit. Prefer a complete word or recognizable abbreviation. For narrower displays, shorten the result/action phrase first, then the task name while retaining its identity. Keep status, the first separator, time/unknown markers, and all four sections. If the fourth section must become very short, retain the progress marker. Do not cut an emoji sequence, half a Chinese phrase, or an English word into meaningless fragments. A UI may still truncate the right side; do not claim fixed columns or guaranteed visibility. When measurement is unavailable, describe width as approximate.

Synthetic examples:

```text
🟢 │ 📄报告整理 │ 18m │ ~60%提纲已定→补引用
🙋 │ 🧪Check │ 42m │ —%need sample
✅ │ 🔧Export │ 12m │ 100%verified
❌ │ 🧪功能验证 │ 12m │ —%本次未达标
```

## Event updates and official tools

Update when this agent handles a meaningful event: start, milestone, waiting/clearance, pause/resume, failure/retry, cancellation, or acceptance. Do not invent a background watcher or promise refreshes while the agent is idle. Avoid polling solely to advance the time field.

Tool availability belongs to the current runtime, not to the Skill. An ordinary task may rename itself when official read/write tools are exposed; it does not require a dot/manager session. A dot/manager context does not by itself authorize other-task writes. Cross-task requests need explicit authorization for the named targets and official access to each. CLI or other sessions without the required official tools are suggestion-only.

1. Resolve the current/requested task identity from trusted runtime context or official discovery, then confirm that exact target with the official read tool (such as `mcp__codex_app__read_thread`) and build the desired title from available evidence. Read the existing title before writing. If it already matches, do not write again.
2. For a requested update, use only the runtime's official title tool (such as `mcp__codex_app__set_thread_title`). For a self-update, use the tool's documented current-target default when supported; confirm that readback addresses the same task. For a specifically authorized other-task update, pass its confirmed identity and backing kind. Do not rename unrelated tasks.
3. Read the same target back. Only a matching title confirms the update. If the write outcome is uncertain, read before considering another write. If readback fails or differs, report the proposed title and unconfirmed result, then stop rather than overwrite blindly.

If a required official read/write tool or target access is missing, provide a suggested title and name the missing capability. Do not edit a database, use UI automation, call private endpoints, or substitute an unofficial command to bypass missing title tools. Never claim a suggestion was applied.

For behavioral review or changes to this convention, use [acceptance cases](references/acceptance-cases.md). The examples are synthetic; public examples and demonstrations must not contain private task names, timelines, paths, accounts, addresses, or thread identifiers.
