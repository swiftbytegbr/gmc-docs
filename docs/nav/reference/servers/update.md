# Update Server

Trigger a game server update (e.g., pull latest game build/mods depending on backend).

- Method: POST
- Path (REST): `/server/{serverId}/update`
- Returns: 200 OK
- Backend behavior: Triggers an update; requires the server to be OFFLINE. The node performs the update asynchronously.

## Responses
- 200 OK: Update requested.
- 403 Forbidden: `missingPermission.MANAGE_SERVERS` — you lack the permission to manage servers in this team.
- 404 Not Found: `general.not_found` — server not found or not in your team.
- 409 Conflict: `server.is_not_offline` — update requires OFFLINE.
- 409 Conflict: `server.server_directory_change_in_progress` — a server directory change task is running on this server.

=== "Java"

    ```java
    gmc.serverClient().updateServer("srv-123").execute();
    ```

=== "JavaScript"

    ```ts
    await gmc.serverClient.updateServer('srv-123');
    ```

=== "Python"

    ```python
    gmc.server_client.update_server('srv-123')
    ```

=== "REST"

    ```bash
    curl -X POST -H "Application-Token: $GMC_APP_TOKEN" \
      https://api.gamemanager.cloud/server/srv-123/update
    ```
