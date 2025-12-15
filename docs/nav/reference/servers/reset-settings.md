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
    await gmc.serverClient.resetSettings('srv-123');
    ```

=== "Python"

    ```python
    gmc.server_client.reset_settings('srv-123')
    ```

=== "REST"

    ```bash
    curl -X POST -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
      https://api.gamemanager.cloud/server/srv-123/reset-settings
    ```

## Responses
- 200 OK: Settings reset requested.
- 403 Forbidden: `missingPermission.MANAGE_SERVERS` — you lack the permission to manage servers in this team.
- 404 Not Found: `general.not_found` — server not found or not in your team.
- 400 Bad Request: `server.unsupported_game_type` — no handler for the server’s game type.