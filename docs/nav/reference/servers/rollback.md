# Rollback Server

Roll a server back to a backup. Optionally restore player-related data.

- Method: POST
- Path (REST): `/server/{serverId}/rollback`
- Body: `{ "backupId": "<id>", "rollbackPlayers": true }`
- Returns: 200 OK
- Backend behavior: Creates a task to restore from the selected backup; downtime expected while files are replaced.

## Responses
- 200 OK: Rollback requested.
- 403 Forbidden: `missingPermission.MANAGE_SERVERS` — you lack the permission to manage servers in this team.
- 404 Not Found: `general.not_found` — server not found or not in your team.
- 409 Conflict: `server.is_not_offline` — rollback requires OFFLINE.
- 409 Conflict: `server.server_directory_change_in_progress` — a server directory change task is running on this server.
- 409 Conflict: `server.backup_directory_change_in_progress` — the node is currently changing the backups directory.

=== "Java"

    ```java
    gmc.serverClient().rollbackServer("srv-123", "backup-1", true).execute();
    ```

=== "JavaScript"

    ```ts
    await gmc.serverClient.rollbackServer('srv-123', 'backup-1', true);
    ```

=== "Python"

    ```python
    gmc.server_client.rollback_server('srv-123', 'backup-1', True)
    ```

=== "REST"

    ```bash
    curl -X POST -H "Content-Type: application/json" \
      -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
      -d '{"backupId":"backup-1","rollbackPlayers":true}' \
      https://api.gamemanager.cloud/server/srv-123/rollback
    ```
