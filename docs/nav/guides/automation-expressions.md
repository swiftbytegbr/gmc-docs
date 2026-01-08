Title: Automation Expression Language (AEL)

What Is AEL?
- AEL is the mini-language you use inside curly braces `{ ... }` to personalize automation steps. It lets you pull in data about the automation, its current run and step, the selected targets, and outputs captured from RCON.
- It’s designed for real users first: readable, forgiving with nulls, and focused on the properties you actually need. Under the hood it uses a safe subset of SpEL.

Who Should Read This
- New users learning how to write Notify/Discord/RCON templates.
- Power users wanting the full catalog of variables and functions.
- Developers integrating editors or doing validation/autocomplete.

At A Glance
- Write `{automation.name}`, `{targets.all.size}`, `{step.indexHuman}`, `{join(targets.all.names, ', ')}` directly in any “Template supported” field.
- If a value is missing/null, it renders as empty. Provide fallbacks with `{value ?: 'n/a'}`.
- Only the documented variables and functions here are available (no arbitrary class/method access).

---

Quick Start (3 minutes)
1) Say hello
```
Hello {automation.name}! We are on step {step.indexHuman}/{run.workflowSize}.
```
2) List targets
```
Targets ({targets.all.size}): {join(targets.all.names, ', ')}
```
3) Show results
```
OK: {targets.succeeded.size} — {join(targets.succeeded.names, ', ')}
KO: {targets.failed.size} — {join(targets.failed.names, ', ')}
```

Tip: Use a small manual run to preview your template safely before rolling it out broadly.

---

Where You Can Use AEL
- Notify step: title, message
- Discord Webhook step: content and all embed text fields
- RCON Command step: command (and later consume captured output)
- Stop step: message
- Backup step: backupName
- Setting Sync step: string values in key sets

Note: Timed/State waits and start/restart/update are numeric or enum inputs; templates typically aren’t used there.

---

Concepts You’ll Use
- Property‑first access: use properties, not method calls. Example: `{targets.names}`, not `targets.names()`.
- Null‑safe rendering: null inside text becomes empty. Use defaults with the Elvis operator: `{maybe ?: 'n/a'}`.
- Collections: filter with `.?[cond]`, transform with `.![expr]`, index with `[i]`, get size with `.size()`.
- Safe navigation: `obj?.prop` yields null if `obj` is null.

---

Syntax Reference

Literals
- Strings: `'text'` or `"text"` (escape quotes inside the other), numbers: `42`, `3.14`, booleans: `true`/`false`, `null`.

Arithmetic and Comparison
- Arithmetic: `{1 + 2}`, `{5 % 2}`
- Comparison: `{targets.all.size > 5}`, `{automation.name == 'Nightly Restart'}`

Boolean Logic
- `{targets.all.size > 0 and run.workflowSize >= 1}`
- `{(teamName != null) or (targets.succeeded.size > 0)}`

Conditionals
- Ternary: `{targets.all.size > 0 ? 'has targets' : 'none'}`
- Elvis (default when null/empty): `{backupName ?: 'unnamed'}`

Safe Navigation
- Use `?.` to avoid errors when something might be null:
```
{outputs?.rcon('cap')?.byId(targets.all.ids[0])?.response}
```

Collections
- Size: `{targets.all.names.size()}`
- Index: `{targets.all.names[0]}`
- Filter (selection):
```
{join(targets.all.names.?[#this.startsWith('EU-')], ', ')}
```
- Map (projection):
```
{join(targets.all.names.![upper(#this)], ', ')}
```

Strings
- Concatenate: `{'Hello ' + automation.name}`
- Trim/Case/Join: `{trim('  hi  ')}`, `{upper(teamName)}`, `{join(targets.all.names, ', ')}`

---

## Complete Variable Catalog

### Convenience values

| Path | Type | Description |
| --- | --- | --- |
| `teamName` | String | Team display name |
| `nowIso` | String | Current time ISO‑8601 (UTC) |
| `epoch` | long | Current epoch seconds |
| `date` | String | UTC date `yyyy‑MM‑dd` |
| `timeHms` | String | UTC time `HH:mm:ss` |

### Automation

| Path | Type | Description |
| --- | --- | --- |
| `automation.id` | String | Automation ID |
| `automation.teamId` | String | Team ID |
| `automation.name` | String | Name |
| `automation.description` | String | Description |
| `automation.enabled` | boolean | Enabled flag |
| `automation.createdAt` | Instant | Creation time |
| `automation.updatedAt` | Instant | Last update time |

### Run

| Path | Type | Description |
| --- | --- | --- |
| `run.id` | String | Run ID |
| `run.automationId` | String | Owning automation |
| `run.teamId` | String | Team ID |
| `run.status` | enum | `QUEUED|PENDING|RUNNING|SUCCEEDED|FAILED|CANCELED|TIMEOUTED` |
| `run.createdAt` | Instant | Created |
| `run.startedAt` | Instant | Started (nullable) |
| `run.finishedAt` | Instant | Finished (nullable) |
| `run.workflowSize` | int | Number of steps |

### Step

| Path | Type | Description |
| --- | --- | --- |
| `step.index` | Integer | 0‑based index of current step |
| `step.indexHuman` | String | 1‑based for display |
| `step.type` | enum | Current step type |
| `step.startedAt` | Instant | Step start time (nullable) |
| `step.finishedAt` | Instant | Step end time (nullable) |

### Targets (bucketed)

| Path | Type | Description |
| --- | --- | --- |
| `targets.all.ids` | List<String> | All target IDs (stable order) |
| `targets.all.names` | List<String> | Display names aligned to `ids` |
| `targets.all.size` | int | Number of total targets |
| `targets.all.count` | int | Alias for `size` |
| `targets.active.ids` | List<String> | IDs still active for current step |
| `targets.active.names` | List<String> | Names aligned to `active.ids` |
| `targets.active.size` | int | Count of active targets |
| `targets.succeeded.ids` | List<String> | IDs marked SUCCEEDED for current step |
| `targets.succeeded.names` | List<String> | Names aligned to `succeeded.ids` |
| `targets.succeeded.size` | int | Count of succeeded targets |
| `targets.failed.ids` | List<String> | IDs FAILED for this step or globally skipped |
| `targets.failed.names` | List<String> | Names aligned to `failed.ids` |
| `targets.failed.size` | int | Count of failed/skipped targets |
| `targets.nameById(id)` | String|null | Lookup display name by server ID |

 

### Outputs (RCON)

| Path | Type | Description |
| --- | --- | --- |
| `outputs.rcon(name)` | RconSet | Access captured responses by capture name |
| `outputs.rcon(name).responses` | List<String> | All responses for that capture |
| `outputs.rcon(name).byId(serverId)` | RconEntry | Entry for a specific target |
| `...byId(...).response` | String|null | Captured response for that target |
| `...byId(...).present` | boolean | True if a response exists |

Notes
- Lists are aligned by index (e.g., `ids[i]` ↔ `names[i]`). Ordering is stable across the step.
- Nulls render empty inside strings. Use `{something ?: 'n/a'}` for a default.

---

Function Catalog (with examples)

Strings

| Function | Returns | Example |
| --- | --- | --- |
| `upper(s)` | String | `{upper(automation.name)}` → `NIGHTLY RESTART` |
| `lower(s)` | String | `{lower(teamName)}` |
| `trim(s)` | String | `{trim('  hello  ')}` → `hello` |
| `join(list, sep)` | String | `{join(targets.all.names, ', ')}` |

Time

| Function | Returns | Example |
| --- | --- | --- |
| `formatDate(epochSeconds, pattern, zone)` | String | `{formatDate(epoch, 'yyyy-MM-dd HH:mm', 'UTC')}` |

Math (double)

| Function | Returns | Example |
| --- | --- | --- |
| `min(a,b)` | double | `{min(3.5, 2)}` → `2.0` |
| `max(a,b)` | double | `{max(targets.all.size, 10)}` |
| `sum(a,b)` | double | `{sum(1.5, 2.5)}` → `4.0` |
| `avg(a,b)` | double | `{avg(2, 10)}` → `6.0` |

---

RCON Capture & Smart Awaiting
1) In your RCON step, set `var` to a capture name (e.g., `cap`).
2) In a later step, reference the capture to read responses:
```
All responses:\n{join(outputs.rcon('cap').responses, '\n---\n')}
```
3) Awaiting modes
- AUTO (default): the executor scans subsequent steps and awaits only when `{outputs.rcon('cap')...}` is referenced.
- ALWAYS: force awaiting, even if no later template references it.
- NEVER: never await (fire‑and‑forget).

Timeouts
- Optional `timeoutMs` lets you control how long to wait. If it expires, targets are marked FAILED with a timeout message. Late responses can still be persisted.

---

Recipes by Step Type

Notify
```
Title:  {automation.name} — step {step.indexHuman}/{run.workflowSize}
Message: Targets ({targets.all.size}): {join(targets.all.names, ', ')}\n
Succeeded ({targets.succeeded.size}): {join(targets.succeeded.names, ', ')}\n
Failed ({targets.failed.size}): {join(targets.failed.names, ', ')}
```

Discord Webhook (content)
```
Run {automation.name} on {date} at {timeHms} (UTC)\n
Targets: {targets.all.size} — {join(targets.all.names, ', ')}
```

Discord Webhook (embed fields)
```
Title:       {automation.name} — Step {step.indexHuman}
Description: Targets ({targets.all.size}): {join(targets.all.names, ', ')}
Field name:  Succeeded
Field value: {targets.succeeded.size} — {join(targets.succeeded.names, ', ')}
Field name:  Failed
Field value: {targets.failed.size} — {join(targets.failed.names, ', ')}
```

RCON summary (after capture `cap`)
```
{join(outputs.rcon('cap').responses, '\n---\n')}
```

Stop (conditional message)
```
{targets.all.size > 3 ? 'Rolling stop' : 'Quick stop'} on {targets.all.size} servers
```

Backup naming
```
{automation.name}-{date}-{timeHms}
```

Setting Sync (example string values)
```
WelcomeMessage = Hello {teamName}! Run {automation.name} on {date}.
```

 

---

Troubleshooting Guide
- Empty output? The value is null. Add a default: `{value ?: 'n/a'}`.
- “Unknown property/function”? Check spelling and use properties (no `()` unless calling a listed function).
- “Index out of bounds”? Ensure the list has items before `[0]`, or guard with a conditional.
- “Did not await RCON”? Ensure you reference `{outputs.rcon('cap')...}` in a later step, or set `awaitMode=ALWAYS`.

---

Security & Performance
- Expressions run in a restricted sandbox. Only the variables and functions above are available; no static methods or reflection.
- Keep expressions short and focused. Use `join(...)` for lists. Avoid heavy projections or deeply nested expressions.

---

 

Appendix: Operators Cheatsheet

| Category | Examples | Notes |
| --- | --- | --- |
| Arithmetic | `1 + 2`, `5 % 2` | Standard precedence |
| Comparison | `a == b`, `a != b`, `a > b`, `a >= b`, `a < b`, `a <= b` | Works for numbers/strings |
| Boolean | `a and b`, `a or b`, `not a` | Short‑circuiting |
| Conditional | `cond ? x : y` | Branch based on boolean |
| Elvis | `a ?: b` | Use `b` if `a` is null/empty |
| Safe nav | `obj?.prop` | Yields null if `obj` is null |
| Collections | `list.size()`, `list[i]`, `list.?[cond]`, `list.![expr]` | Select/filter/map |
