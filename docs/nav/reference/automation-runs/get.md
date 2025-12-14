# Get Automation Run

Fetch a single automation run by ID.

- Method: GET
- Path (REST): `/automation-run/{runId}`
- Returns: AutomationRun

=== "Java"
```java
var run = client.automationRunClient().getRun("run-1").execute();
```

=== "JavaScript"
```ts
const run = await client.automationRunClient.getRun('run-1');
```

=== "Python"
```python
run = client.automation_run_client.get_run('run-1')
```

=== "REST"
```bash
curl -s -H "Application-Token: $GMC_APP_TOKEN" \
  https://api.gamemanager.cloud/automation-run/run-1
```
