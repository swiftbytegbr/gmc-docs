# Model: Automation

Defines a reusable workflow to operate your infrastructure.

Fields:
- `id` (string), `teamId` (string)
- `name` (string), `description` (string)
- `enabled` (boolean)
- `createdAt`, `updatedAt` (ISO datetime)
- `targets` (TargetSelector): which resources to act on
- `workflow` (AutomationStep[]): ordered steps
- `trigger` (AutomationTrigger): automatic trigger config (optional)
- `runTimeoutSec` (int): overall run timeout

Example:
```json
{
  "id": "auto-1",
  "teamId": "team-1",
  "name": "Nightly Restart",
  "description": "Restart servers every night",
  "enabled": true,
  "createdAt": "2025-01-01T00:00:00Z",
  "updatedAt": "2025-01-02T00:00:00Z",
  "targets": { /* target selector */ },
  "workflow": [ /* steps */ ],
  "trigger": { /* schedule */ },
  "runTimeoutSec": 1800
}
```
