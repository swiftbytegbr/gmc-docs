# List Automation Runs

List runs for your team with optional filters.

- Method: GET
- Path (REST): `/automation-run/by-team/{teamId}` with query parameters
- Returns: `Page<AutomationRun>`
- Filters: `page`, `size`, `automationId`, `statuses`, `createdFrom`, `createdTo`

## Response
Example page payload:
```json
{
  "content": [
    {
      "id": "run-1",
      "automationId": "auto-1",
      "teamId": "team-1",
      "status": "RUNNING",
      "createdAt": "2025-01-02T00:00:00Z",
      "startedAt": "2025-01-02T00:00:05Z",
      "finishedAt": null,
      "targetIds": { "srv-1": true },
      "currentStep": {},
      "stepHistory": [],
      "cancelRequested": false,
      "workflowSize": 3
    }
  ],
  "page": 0,
  "size": 25,
  "totalElements": 1,
  "totalPages": 1,
  "first": true,
  "last": true,
  "numberOfElements": 1,
  "empty": false
}
```

=== "Java"

    ```java
    Page<AutomationRun> runs = client.automationRunClient()
        .listRuns(0, 25, null, null, null, null)
        .execute();
    ```

=== "JavaScript"

    ```ts
    const runs = await client.automationRunClient.listRuns(0, 25, { /* filters */ });
    ```

=== "Python"

    ```python
    runs = client.automation_run_client.list_runs(page=0, size=25)
    ```

=== "REST"

    ```bash
    curl -s -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
      "https://api.gamemanager.cloud/automation-run/by-team/$TEAM_ID?page=0&size=25"
    ```
