# List Automations

List automations defined for your team.

- Method: GET
- Path (REST): `/automation/by-team/{teamId}`
- Returns: Array of Automation

=== "Java"

    ```java
    java.util.List<Automation> list = client.automationClient().listAutomations().execute();
    ```

=== "JavaScript"

    ```ts
    const list = await client.automationClient.listAutomations();
    ```

=== "Python"

    ```python
    automations = client.automation_client.list_automations()
    ```

=== "REST"

    ```bash
    curl -s -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
      https://api.gamemanager.cloud/automation/by-team/$TEAM_ID
    ```
