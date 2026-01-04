Title: Automation Expression Language (AEL)

Overview
- AEL provides typed, property-first expressions for templates in Notify and Discord steps.
- Use `#{ ... }` in template strings. Legacy `{ ... }` is accepted and auto-converted.

Core Objects
- `automation`: id, teamId, name, description, enabled, createdAt, updatedAt
- `run`: id, automationId, teamId, status, createdAt, startedAt, finishedAt, workflowSize
- `step`: index (0-based), indexHuman (1-based), type, startedAt, finishedAt
- `targets`: count; lists `ids`, `names`, `activeIds`, `activeNames`, `succeededIds`, `succeededNames`, `failedIds`, `failedNames`; lookup `nameById(id)`
- `outputs`: `rcon(name)` → `.byId(serverId).response`, `.responses`
- Convenience: `teamName`, `nowIso`, `epoch`, `date`, `timeHms`

Functions
- Strings: `upper(s)`, `lower(s)`, `trim(s)`, `join(list, sep)`
- Time: `formatDate(epochSeconds, pattern, zone)`
- Math: `min(a,b)`, `max(a,b)`, `sum(a,b)`, `avg(a,b)`

Examples
- `Hello #{automation.name}`
- `Targets: #{targets.count}`
- `Succeeded: #{targets.succeededIds.size()}`
- `Failed: #{join(targets.failedNames, ', ')}`
- `#{outputs.rcon('myRcon').byId(targets.ids.get(0)).response}`
- `#{join(outputs.rcon('myRcon').responses, '; ')}`

Errors
- If a template expression cannot be parsed or evaluated, the step fails for all active targets with `automation.expression_error` and no side-effects are performed.

Notes
- Use property access for data (no parentheses), and function calls only when arguments are required.
