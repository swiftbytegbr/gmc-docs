Title: AEL Cheatsheet

Basics
- Embed with `{ ... }` in template fields.
- Nulls render empty; add defaults: `{value ?: 'n/a'}`.
- Safe navigation: `obj?.prop`.

Top Symbols
- `automation`: `id`, `name`, `teamId`, `enabled`, `createdAt`, `updatedAt`.
- `run`: `id`, `status`, `workflowSize`, `createdAt`, `startedAt`, `finishedAt`.
- `step`: `index`, `indexHuman`, `type`, `startedAt`, `finishedAt`.
- `targets`: `count`, lists: `ids`, `names`, `activeIds`, `activeNames`, `succeededIds`, `succeededNames`, `failedIds`, `failedNames`; lookup: `nameById(id)`.
- `outputs`: `rcon(name)` → `responses`, `byId(id).response`, `byId(id).present`.
- Convenience: `teamName`, `nowIso`, `epoch`, `date` (UTC yyyy‑MM‑dd), `timeHms` (UTC HH:mm:ss).

Functions
- Strings: `upper(s)`, `lower(s)`, `trim(s)`, `join(list, ', ')`.
- Time: `formatDate(epoch, 'yyyy-MM-dd HH:mm', 'UTC')`.
- Math: `min(a,b)`, `max(a,b)`, `sum(a,b)`, `avg(a,b)`.

Collections
- Size: `list.size()`; Index: `list[0]`.
- Filter: `list.?[cond]` (e.g., `targets.names.?[#this.startsWith('M')]`).
- Map: `list.![expr]` (e.g., `targets.names.![upper(#this)]`).

Snippets
- Greeting: `Hello {automation.name} – step {step.indexHuman}/{run.workflowSize}`
- Targets: `{targets.count} servers: {join(targets.names, ', ')}`
- Succeeded: `{targets.succeededIds.size()} ok: {join(targets.succeededNames, ', ')}`
- Time: `Now {formatDate(epoch, 'HH:mm:ss', 'Europe/Berlin')}`
- RCON all: `{join(outputs.rcon('cap').responses, '\\n---\\n')}`
- RCON first: `{outputs.rcon('cap').byId(targets.ids[0]).response ?: 'no response'}`

Gotchas
- Do not call properties as methods (`targets.ids`, not `targets.ids()`).
- Quote capture names in `outputs.rcon('...')`.
- Any expression failure fails the step; side‑effects are skipped.
