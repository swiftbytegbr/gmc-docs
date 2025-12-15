# Delete Backup

Delete a specific backup by its ID.

- Method: POST
- Path (REST): `/server/{serverId}/delete-backup`
- Body: `{ "backupId": "<id>" }`
- Returns: 200 OK
- Backend behavior: Removes backup metadata and data on the node.

=== "Java"

    ```java
    gmc.serverClient().deleteBackup("srv-123", "backup-1").execute();
    ```

=== "JavaScript"

    ```ts
    await gmc.serverClient.deleteBackup('srv-123', 'backup-1');
    ```

=== "Python"

    ```python
    gmc.server_client.delete_backup('srv-123', 'backup-1')
    ```

=== "REST"

    ```bash
    curl -X POST -H "Content-Type: application/json" \
      -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
      -d '{"backupId":"backup-1"}' \
      https://api.gamemanager.cloud/server/srv-123/delete-backup
    ```


## Responses
- 200 OK: Backup deletion requested.
- 403 Forbidden: `missingPermission.MANAGE_SERVERS` — you lack the permission to manage servers in this team.
- 404 Not Found: `general.not_found` — server or backup not found.
- 409 Conflict: `server.state_unknown` — the server is in an unknown state.
- 409 Conflict: `server.backups_empty` — no backups available for this server.
- 409 Conflict: `server.server_directory_change_in_progress` — a server directory change task is running on this server.
- 409 Conflict: `server.backup_directory_change_in_progress` — the node is currently changing the backups directory.
