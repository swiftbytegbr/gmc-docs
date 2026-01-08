Title: Automation Expression Language (AEL)

What is AEL?
- AEL is a typed, property‑first expression language used inside automation templates (Notify, Discord webhook, and future messaging steps).
- It is built on Spring Expression Language (SpEL) and exposes a curated, safe set of properties and functions.
- Goal: make templates easy to write for humans, and easy to auto‑complete for tools.

How to write expressions
- Embed expressions inside strings using `#{ ... }`.
  - Example: `Hello #{automation.name}!`
- Legacy `{ ... }` placeholders are accepted and auto‑converted to `#{ ... }` at render time.
- Property‑first rule: use properties for data (`targets.names`, not `targets.names()`), functions only when arguments are required.

Quick examples
- `Targets: #{targets.count}`
- `First name: #{targets.names[0]}`
- `Succeeded: #{targets.succeededIds.size()}`
- `Failed: #{join(targets.failedNames, ', ')}`
- `RCON: #{outputs.rcon('ping').byId(targets.ids.get(0)).response}`
- `All RCON: #{join(outputs.rcon('ping').responses, '; ')}`

Grammar & operators (SpEL subset)
- Literals: strings ('text' or "text"), numbers (42, 3.14), booleans (true/false), null.
- Arithmetic: `+ - * / %` with usual precedence.
- Comparison: `< <= > >= == !=` (numbers and strings).
- Boolean: `and`, `or`, `not`.
- Conditional: ternary `cond ? a : b`, Elvis `a ?: b`.
- Safe navigation: `obj?.prop` (yields null when `obj` is null).
- Collections:
  - Size: `list.size()`
  - Index: `list[0]`, `list[list.size()-1]`
  - Projection: `list.![upper(#this)]` (transform items)
  - Selection: `list.?[#this != null]` (filter)

Root model (autocomplete spec)
- Top‑level properties:
  - `automation: Automation`
  - `run: AutomationRun`
  - `step: StepView`
  - `targets: TargetsView`
  - `outputs: OutputsView`
  - Convenience: `teamName: String`, `nowIso: String`, `epoch: long`, `date: String`, `timeHms: String`

Type: Automation
- `id: String`, `teamId: String`, `name: String`, `description: String`, `enabled: boolean`
- `createdAt: Instant`, `updatedAt: Instant`

Type: AutomationRun
- `id: String`, `automationId: String`, `teamId: String`, `status: enum`
- `createdAt: Instant`, `startedAt: Instant`, `finishedAt: Instant`, `workflowSize: int`

Type: StepView
- `index: Integer` (0‑based)
- `indexHuman: String` (1‑based for display)
- `type: enum`
- `startedAt: Instant`, `finishedAt: Instant`

Type: TargetsView
- `count: int`
- Ordered lists (stable):
  - `ids: List<String>` — all target IDs
  - `names: List<String>` — display names aligned to `ids`
  - `activeIds`, `activeNames` — currently active for this step
  - `succeededIds`, `succeededNames` — marked SUCCEEDED for this step
  - `failedIds`, `failedNames` — marked FAILED (or globally skipped) for this step
- Lookup: `nameById(id: String): String | null`

Type: OutputsView
- `rcon(name: String): RconSet` — access captured RCON results stored under the given capture name (from the RCON step’s `var`).

Type: RconSet
- `byId(serverId: String): RconEntry`
- `responses: List<String>` — all captured response strings for this capture

Type: RconEntry
- `response: String | null` — response for this specific target
- `present: boolean` — true if a response exists

Global functions (signatures & usage)
- Strings
  - `upper(s: String): String` — `#{upper(automation.name)}`
  - `lower(s: String): String` — `#{lower(teamName)}`
  - `trim(s: String): String` — `#{trim('  hello  ')}`
  - `join(items: Collection<any>, sep: String): String` — `#{join(targets.names, ', ')}`
- Time
  - `formatDate(epochSeconds: long, pattern: String, zone: String): String`
    - `#{formatDate(epoch, 'yyyy-MM-dd HH:mm', 'UTC')}`
- Math (double)
  - `min(a: double, b: double)`, `max(a: double, b: double)`, `sum(a: double, b: double)`, `avg(a: double, b: double)`

Safety and constraints
- Type/class references (SpEL `T(...)`) are not exposed.
- Only documented properties and functions are available.
- Null rendering: a null value inside `#{...}` renders as an empty string in the final output.

Authoring patterns (recipes)
- List formatting
  - `Names: #{join(targets.names, ', ')}`
  - `Succeeded (#{targets.succeededIds.size()}): #{join(targets.succeededNames, ', ')}`
- Conditional blocks
  - `#{targets.failedIds.size() > 0 ? 'Some targets failed' : 'All good'}`
- RCON summaries
  - `Latest: #{outputs.rcon('myRcon').byId(targets.ids.get(0)).response ?: 'no output'}`
  - `All: #{join(outputs.rcon('myRcon').responses, '; ')}`
- Time formatting
  - `Run started: #{formatDate(epoch, 'yyyy-MM-dd HH:mm:ss', 'Europe/Berlin')}`

Common mistakes (and fixes)
- Using `()` on properties: use `targets.ids`, not `targets.ids()`.
- Forgetting quotes in `rcon(name)`: use `'myRcon'` or "myRcon".
- Missing null checks when indexing: ensure lists are non‑empty before accessing `[0]`, or use conditionals.

Debugging & validation
- Start small: print simple properties, then add functions.
- Validate complex expressions in a test/staging run before production.
- On any parse/evaluation error, the step fails with `automation.expression_error` and no side‑effects are sent.

Performance notes
- Keep expressions concise. Prefer `join(...)` to manual loops.
- Avoid heavy computation in templates; precompute in the automation logic when possible.

Security
- Expressions cannot access arbitrary classes or the filesystem; only the documented properties and functions are exposed.

How RCON capture ties in
- In an RCON step, set `var` to a capture name. If a later template references `outputs.rcon('<var>')`, the executor may await responses (AUTO), or you can override with ALWAYS/NEVER.
- Captured responses are exposed to AEL via `outputs.rcon(name)`.

Migration from legacy placeholders
- Old → New mapping:
  - `targets.ids()` → `targets.ids`
  - `targets.names()` → `targets.names`
  - `targets.activeIds()` → `targets.activeIds` (and analogous for names/succeeded/failed)
  - `outputs.rcon('x').responses()` → `outputs.rcon('x').responses`
  - `nowIso()` → `nowIso`, `epoch()` → `epoch`

End‑to‑end example (Discord notification)
```
Title:  #{automation.name} — step #{step.indexHuman}
Body:   Targets (#{targets.count}): #{join(targets.names, ', ')}
        Failed: #{targets.failedIds.size()} — #{join(targets.failedNames, ', ')}
        RCON:   #{join(outputs.rcon('check').responses, '; ')}
```
