# Delete Automation

Delete an automation by ID.

- Method: POST
- Path (REST): `/automation/{automationId}/delete`
- Returns: 204 No Content

=== "Java"
```java
client.automationClient().deleteAutomation("auto-1").execute();
```

=== "JavaScript"
```ts
await client.automationClient.deleteAutomation('auto-1');
```

=== "Python"
```python
client.automation_client.delete_automation('auto-1')
```

=== "REST"
```bash
curl -X POST -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
  https://api.gamemanager.cloud/automation/auto-1/delete
```
