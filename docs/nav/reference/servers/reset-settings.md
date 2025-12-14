# Reset Server Settings

Reset a server's settings to defaults.

- Method: POST
- Path (REST): `/server/{serverId}/reset-settings`
- Returns: 200 OK
- Backend behavior: Rewrites config to defaults. Server restart may be required.

=== "Java"

    ```java
    gmc.serverClient().resetSettings("srv-123").execute();
    ```

=== "JavaScript"

    ```ts
    await client.serverClient.resetSettings('srv-123');
    ```

=== "Python"

    ```python
    client.server_client.reset_settings('srv-123')
    ```

=== "REST"

    ```bash
    curl -X POST -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
      https://api.gamemanager.cloud/server/srv-123/reset-settings
    ```
