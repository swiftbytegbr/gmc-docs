# Get Automation

Fetch a single automation by ID.

- Method: GET
- Path (REST): `/automation/{automationId}`
- Returns: Automation

=== "Java"
```java
var automation = client.automationClient().getAutomation("auto-1").execute();
```

=== "JavaScript"
```ts
const automation = await client.automationClient.getAutomation('auto-1');
```

=== "Python"
```python
automation = client.automation_client.get_automation('auto-1')
```

=== "REST"
```bash
curl -s -H "Application-Token: $GMC_APP_TOKEN" \
  https://api.gamemanager.cloud/automation/auto-1
```
