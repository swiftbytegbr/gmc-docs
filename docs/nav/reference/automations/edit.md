# Edit Automation

Update an existing automation's settings.

- Method: POST
- Path (REST): `/automation/{automationId}/edit`
- Body: `AutomationUpdateRequest`
- Returns: Automation

=== "Java"

    ```java
    var updated = client.automationClient().editAutomation("auto-1", new AutomationUpdateRequest()).execute();
    ```

=== "JavaScript"

    ```ts
    const updated = await client.automationClient.editAutomation('auto-1', { /* fields */ });
    ```

=== "Python"

    ```python
    updated = client.automation_client.edit_automation('auto-1', { /* fields */ })
    ```

=== "REST"

    ```bash
    curl -X POST -H "Content-Type: application/json" \
      -H "Application-Token: $GMC_APP_TOKEN" \
      -d '{"name":"Updated"}' \
      https://api.gamemanager.cloud/automation/auto-1/edit
    ```
