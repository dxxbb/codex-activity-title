# Codex Activity Title · 0.1

**Too many tasks open? See which one is moving, waiting, or actually done.**

A small Codex Skill that turns an Activity title into a compact status line:

```text
status │ project icon + task │ elapsed │ progress + result → current action
```

| Before: a task name | After: a useful status line |
| --- | --- |
| Prepare report | 🔵 │ 📄Report │ 18m │ ~60%outline done→cite |
| Check feature | 🙋 │ 🧪Check │ 42m │ —%need sample |
| Fix export | ✅ │ 🔧Export │ 12m │ 100%verified |

These are invented examples. Percentages are estimates from task milestones; a title is not a live timer.

**Standalone tasks can use it; managed groups have one coordinator title writer.**

| Session / request | Supported behavior |
| --- | --- |
| Ordinary standalone task with an official rename tool and confirmed target access | Can maintain its own requested title |
| Authorized managed group | The coordinator assesses facts and alone writes titles; workers report business facts |
| Coordinator or standalone runtime without an official rename tool | Generates suggestions; the coordinator reports its own management gap |

The current runtime may expose `cloud_threads.rename`, the earlier Codex app title tool, or another documented official surface. Check its actual schema; a tool observed in one coordinator is not guaranteed in ordinary sessions or workers. Installing this Skill adds neither tools nor permissions. Read the existing title when it is exposed and skip identical writes.

A successful official rename response with the exact requested target ID and title is accepted-write evidence. Independent title readback is a separate check. If read/list omit a title field, say the write was accepted and independent verification is unavailable; do not claim matching readback or that the user has seen the change. Do not repeat a successful write merely to cover that verification gap.

![Before and after: 12 generic tasks in 300px dark lists](docs/activity-title-comparison-en.png)

**Example tasks / UI illustration, not a screenshot.** Both lists are 300 logical pixels wide, enlarged together for clarity; the right side can truncate. All 12 tasks match one-to-one. No private activity is included.

Useful when you switch between several Codex tasks and want to identify the next useful step without opening each conversation.

## Install and use

In Codex, ask:

```text
Use skill-installer to install activity-title from
https://github.com/dxxbb/codex-activity-title/tree/main/codex-skill/activity-title
```

Or copy the complete [`codex-skill/activity-title/`](codex-skill/activity-title/) folder into the skills directory your Codex setup uses. The standard local installer defaults to `~/.codex/skills/activity-title/`.

To pin an install, replace `COMMIT_SHA` with a verified revision:

```text
Use skill-installer to install activity-title from
https://github.com/dxxbb/codex-activity-title/tree/COMMIT_SHA/codex-skill/activity-title
```

The helper refuses to overwrite an existing install. For an upgrade, preserve any local edits, then replace the complete installed Skill folder with the chosen new revision. Edit the source package, not an installed copy, when maintaining your own fork.

Then ask:

```text
Use $activity-title for this task. Keep its title current when the task state changes.
```

For a preview without changing a title:

```text
Use $activity-title to suggest a title only.
```

Follow your runtime's skill reload guidance; installation alone does not prove that the current conversation has loaded it. Installing a local Codex Skill does not install it into ChatGPT or another agent runtime.

## What the title tells you

| Status | Meaning |
| --- | --- |
| 📋 | Not started |
| 🔵 | Advancing on the agreed path |
| ⚠️ | A specific deviation needs correction or is being corrected |
| ↪️ | Responsibility transferred to an accepted, started successor |
| ⌛ | Waiting for a dependency or resource |
| 🙋 | Waiting for the user |
| ⏸️ | Deliberately paused |
| ✅ | Delivered within this task's acceptance scope |
| 🚫 | Explicitly cancelled |

A Task is the user's outcome; a Session is its agreed execution scope. Titles display that Session's evidenced facts without silently reducing the Task's goal. Failure/blockage diagnoses remain in its details; the owner must establish the next disposition. Correction needs a specific deviation, owner, action and review point, and restores the actual state only after effective review. Confirmed transfer requires a successor that accepted and started; it does not mean accepted delivery.

Elapsed time covers the named Session from its first trustworthy start, including corrections and waits. It freezes when that responsibility ends through scoped acceptance, confirmed transfer or explicit cancellation. Unknown time is `?m`; unknown progress is `—%`. Estimated progress has a `~`; `100%` requires acceptance of the specific deliverable. An idle runtime does not mean a task is delivered.

The Skill follows the user's language, keeps task identity stable, and shortens result/action phrases before the task name. It uses the default proportional font with no padding or font installation. English words and emoji stay intact.

## Limits

- Updates require an official rename tool and authorized target access. Existing-title comparison and independent readback use actual title fields when available; absent fields stay an explicit verification gap. Without rename capability, the Skill gives a suggestion.
- Updates happen when the agent handles a task event. There is no background watcher, live clock, native dashboard, or fixed-width layout.
- A narrow Activity list may still truncate the right side. This is a plain text title, not four separately styled columns.
- Missing status evidence is reported outside the title; the Skill does not guess a status or equate a failed experiment with a failed project.

The public Skill folder is the maintained source. Installed copies are projections of a chosen revision. No personal task history is included.

## Checks

An ordinary task's default-current-target rename and matching official readback were verified with app tools exposed. An authorized coordinator also successfully used the dynamically exposed official `cloud_threads.rename`, which returned the requested IDs and titles; its read/list surface omitted an independent title field. These observations establish those specific capabilities and evidence boundaries, not universal availability, independent readback of every write or UI visibility.

The self-contained [acceptance cases](codex-skill/activity-title/references/acceptance-cases.md) cover task-wide elapsed time, ended-scope freezing, failure dispositions, correction/review, confirmed transfer, unknown data, milestone progress, Chinese/English width, idempotent updates, and unavailable or mismatching tool responses. They are synthetic behavioral checks, not a promise of automatic UI or background testing.

## 中文

**任务开多了，哪项在推进、哪项在等人、哪项真的完成？**

![12项通用任务的深色Activity标题前后对比](docs/activity-title-comparison-zh.png)

**示例任务 / 界面示意，不是截图。** 两列同为300逻辑像素，整体放大便于查看，12项任务一一对应；右侧保留截断，没有单独撑宽列表。

这个小 Skill 把 Codex Activity 标题变成四区状态栏：

```text
状态 │ 项目图标短任务 │ 耗时 │ 估算%已达成→当前动作
🔵 │ 📄报告整理 │ 18m │ ~60%提纲已定→补引用
🙋 │ 🧪功能验证 │ 42m │ —%等待样本
✅ │ 🔧导出修复 │ 12m │ 100%验收通过
```

英文 Skill 正文是执行规范，输出优先遵循用户明确指定的语言，否则沿用当前任务的交流语言；英文安装代码块不会把标题强制改成英文。可用中文安装：“用 skill-installer 从本仓库的 codex-skill/activity-title 安装 activity-title”；使用：“用 $activity-title，在任务状态变化时更新当前标题”。

以上都是合成示例。普通独立 Session 有官方改名工具和确认的目标访问能力时，可维护自己的标题，不要求 dot。管理一组任务时，由获授权的协调者统一判断状态、构造和写入标题；业务 worker 只回报事实，不自行改标题、不发现标题工具，也不被标题消息打断。协调者缺工具时由协调者报告，不下放给 worker。安装 Skill 不会增加工具或权限。只想看候选，就说“只建议标题，不修改”。

当前运行时可能暴露官方 `cloud_threads.rename` 或其他官方标题入口，须以实际 schema 为准，不能由管理端的成功推断普通 Session 都有。成功写入返回 exact ID/title 是官方写入回执；独立回读是另一层证据。read/list 没有标题字段时，明确报告“写入成功、独立回读不可用”，不宣称已独立读回或用户已看到，也不重复覆盖成功的写入。

🔵 表示正常推进；⚠️ 表示具体偏差待纠正或正在纠偏，须有负责人、动作与复核点，复核有效才恢复真实状态；↪️ 须有真实承接并已开始的后继。需用户协助用 🙋，等具体外部条件用 ⌛，明确暂停用 ⏸️。失败与阻塞是详情里的临时诊断，负责人仍须落实处置，不能永久留叉或擅自取消。已验收的旧 Session 保留 ✅，转交本身不代表验收。

耗时对应标题这项 Session 范围的首次开始，包含纠偏与等待；验收、真实转交或明确取消使该范围责任结束后才冻结。未知写 `?m` / `—%`，进度估算带 `~`，具体交付通过验收才显示 `100%`。它按事件更新，不是后台实时计时器；默认比例字体，窄列表仍可能省略右侧文字。

MIT licensed. Independent community project; not affiliated with OpenAI.
