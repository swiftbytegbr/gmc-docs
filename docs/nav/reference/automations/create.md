# Create Automation

Create a new automation.

- Method: POST
- Path (REST): `/automation/create`
- Body: `AutomationCreateRequest`
- Returns: Automation
- Backend behavior: Validates team ownership and request fields. New automation becomes available for runs.

=== "Java"
```java
var req = new AutomationCreateRequest();
req.setTeamId(client.getTeamId());
req.setName("Nightly Restart");
var created = client.automationClient().createAutomation(req).execute();
```

=== "JavaScript"
```ts
const created = await client.automationClient.createAutomation({ teamId: client.teamId!, name: 'Nightly Restart' });
```

=== "Python"
```python
created = client.automation_client.create_automation({ 'teamId': client.team_id, 'name': 'Nightly Restart' })
```

=== "REST"
```bash
curl -X POST -H "Content-Type: application/json" \
  -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
  -d '{"teamId":"'$TEAM_ID'","name":"Nightly Restart"}' \
  https://api.gamemanager.cloud/automation/create
```
