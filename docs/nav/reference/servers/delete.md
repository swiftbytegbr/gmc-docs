# Delete Server

Permanently delete a server.

- Method: POST
- Path (REST): `/server/{serverId}/delete`
- Body: `{ "forceDelete": false }`
- Returns: 200 OK
- Backend behavior: Deletes the server. Requires OFFLINE unless `forceDelete` is true. With `forceDelete`, the backend immediately removes the server and its profile; otherwise, a delete task is sent to the node.



=== "Java"

    ```java
    gmc.serverClient().deleteServer("srv-123", false).execute();
    ```

=== "JavaScript"

    ```ts
    await gmc.serverClient.deleteServer('srv-123', false);
    ```

=== "Python"

    ```python
    gmc.server_client.delete_server('srv-123', False)
    ```

=== "REST"

    ```bash
    curl -X POST -H "Content-Type: application/json" \
      -H "Application-Token: $GMC_APP_TOKEN" \
      -d '{"forceDelete":false}' \
      https://api.gamemanager.cloud/server/srv-123/delete
    ```

## Responses
- 200 OK: Delete requested (or already deleted when forced).
- 403 Forbidden: `missingPermission.MANAGE_SERVERS` — you lack the permission to manage servers in this team.
- 404 Not Found: `general.not_found` — server not found or not in your team.
- 409 Conflict: `server.is_not_offline` — delete requires OFFLINE when `forceDelete` is false.
- 409 Conflict: `server.server_directory_change_in_progress` — a server directory change task is running (only checked when not forcing).