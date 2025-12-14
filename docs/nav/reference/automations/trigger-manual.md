# Trigger Manual

Trigger an automation manually.

- Method: POST
- Path (REST): `/automation/{automationId}/trigger-manual`
- Body: `ManualTriggerRequest`
- Returns: AutomationRun
- Backend behavior: Enqueues a run; inspect via Automation Runs endpoints.

=== "Java"

    ```java
    AutomationRun run = client.automationClient().triggerManual("auto-1", new ManualTriggerRequest()).execute();
    ```

=== "JavaScript"

    ```ts
    const run = await client.automationClient.triggerManual('auto-1', { targetIds: [] });
    ```

=== "Python"

    ```python
    run = client.automation_client.trigger_manual('auto-1', { 'targetIds': [] })
    ```

=== "REST"

    ```bash
    curl -X POST -H "Content-Type: application/json" \
      -H "Application-Token: $GMC_APP_TOKEN" \
      -d '{"targetIds":[]}' \
      https://api.gamemanager.cloud/automation/auto-1/trigger-manual
    ```
