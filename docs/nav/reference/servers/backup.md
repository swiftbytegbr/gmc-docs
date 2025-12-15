# Backup Server

Create a named backup of a server.

- Method: POST
- Path (REST): `/server/{serverId}/backup`
- Body: `{ "name": "<backup-name>" }`
- Returns: 200 OK
- Backend behavior: Stores a backup of the server's data on the node. The request returns immediately; creation runs asynchronously (track via node task or backup events).


Note: When the team backup limit is reached, the backend automatically deletes the oldest backup.

=== "Java"

    ```java
    gmc.serverClient().backupServer("srv-123", "pre-update").execute();
    ```

=== "JavaScript"

    ```ts
    await gmc.serverClient.backupServer('srv-123', 'pre-update');
    ```

=== "Python"

    ```python
    gmc.server_client.backup_server('srv-123', 'pre-update')
    ```

=== "REST"

    ```bash
    curl -X POST -H "Content-Type: application/json" \
      -H "Application-Token: $GMC_APP_TOKEN" \
      -d '{"name":"pre-update"}' \
      https://api.gamemanager.cloud/server/srv-123/backup
    ```

## Responses
- 200 OK: Backup requested.
- 403 Forbidden: `missingPermission.MANAGE_SERVERS` — you lack the permission to manage servers in this team.
- 404 Not Found: `general.not_found` — server not found or not in your team.
- 409 Conflict: `server.state_unknown` — the server is in an unknown state.
- 409 Conflict: `server.server_directory_change_in_progress` — a server directory change task is running on this server.
- 409 Conflict: `server.backup_directory_change_in_progress` — the node is currently changing the backups directory.