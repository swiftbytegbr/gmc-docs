# List Automation Runs

List runs for your team with optional filters.

- Method: GET
- Path (REST): `/automation-run/by-team/{teamId}` with query parameters
- Returns: `Page<AutomationRun>`
- Filters: `page`, `size`, `automationId`, `statuses`, `createdFrom`, `createdTo`

=== "Java"
```java
var runs = client.automationRunClient().listRuns(0, 25, null, null, null, null).execute();
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
