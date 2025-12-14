# Get Action Log

Retrieve a paginated action log for your team.

- Method: GET
- Path (REST): `/team/{teamId}/action-log?page=0&size=25`
- Returns: `Page<ActionLogItem>`
- Backend behavior: Read-only audit history; useful for traceability.

=== "Java"

    ```java
    de.swiftbyte.gmc.sdk.model.common.Page<ActionLogItem> page = client.teamClient().getActionLog(0, 25).execute();
    ```

=== "JavaScript"

    ```ts
    const page = await client.teamClient.getActionLog(0, 25);
    ```

=== "Python"

    ```python
    page = client.team_client.get_action_log(page=0, size=25)
    ```

=== "REST"

    ```bash
    curl -s -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
      "https://api.gamemanager.cloud/team/$TEAM_ID/action-log?page=0&size=25"
    ```
