# Model: AutomationRun

Represents a single execution of an automation.

Fields:
- `id`, `automationId`, `teamId`
- `status` (enum): `QUEUED`, `PENDING`, `RUNNING`, `SUCCEEDED`, `FAILED`, `CANCELED`, `TIMEOUTED`
- `createdAt`, `startedAt`, `finishedAt`, `scheduledFireAt`
- `targetIds` (map<string, boolean>): current targets still active in the workflow
- `currentStep` (StepState): active step state
- `stepHistory` (StepState[]): completed steps
- `cancelRequested` (boolean)
- `workflowSize` (int)

Example:
```json
{
  "id": "run-1",
  "automationId": "auto-1",
  "teamId": "team-1",
  "status": "RUNNING",
  "createdAt": "2025-01-02T00:00:00Z",
  "startedAt": "2025-01-02T00:00:05Z",
  "finishedAt": null,
  "targetIds": { "srv-1": true, "srv-2": true },
  "currentStep": { /* step metadata */ },
  "stepHistory": [],
  "cancelRequested": false,
  "workflowSize": 3
}
```
