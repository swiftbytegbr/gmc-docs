# Change Server Directory

Set a new directory path for the server's files.

- Method: POST
- Path (REST): `/server/{serverId}/change-directory`
- Body: `{ "serverDirectory": "/servers/cs2" }`
- Returns: 200 OK
- Backend behavior: Creates a task on the node to apply the directory change. A restart may be required to take effect.

## Responses
- 200 OK: Directory change requested.
- 403 Forbidden: `missingPermission.MANAGE_SERVERS` — you lack the permission to manage servers in this team.
- 404 Not Found: `general.not_found` — server not found or not in your team.
- 400 Bad Request: `server.invalid_directory` — invalid or blank directory path.
- 400 Bad Request: `validation.failed` — invalid JSON body.
- 409 Conflict: `server.is_not_offline` — directory change requires OFFLINE.

=== "Java"

    ```java
    gmc.serverClient().changeDirectory("srv-123", "/servers/cs2").execute();
    ```

=== "JavaScript"

    ```ts
    await gmc.serverClient.changeDirectory('srv-123', '/servers/cs2');
    ```

=== "Python"

    ```python
    gmc.server_client.change_directory('srv-123', '/servers/cs2')
    ```

=== "REST"

    ```bash
    curl -X POST -H "Content-Type: application/json" \
      -H "Application-Token: $GMC_APP_TOKEN" \
      -d '{"serverDirectory":"/servers/cs2"}' \
      https://api.gamemanager.cloud/server/srv-123/change-directory
    ```
