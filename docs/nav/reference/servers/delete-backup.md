# Delete Backup

Delete a specific backup by its ID.

- Method: POST
- Path (REST): `/server/{serverId}/delete-backup`
- Body: `{ "backupId": "<id>" }`
- Returns: 200 OK
- Backend behavior: Removes backup metadata and data.

=== "Java"

    ```java
    client.serverClient().deleteBackup("srv-123", "backup-1").execute();
    ```

=== "JavaScript"

    ```ts
    await client.serverClient.deleteBackup('srv-123', 'backup-1');
    ```

=== "Python"

    ```python
    client.server_client.delete_backup('srv-123', 'backup-1')
    ```

=== "REST"

    ```bash
    curl -X POST -H "Content-Type: application/json" \
      -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
      -d '{"backupId":"backup-1"}' \
      https://api.gamemanager.cloud/server/srv-123/delete-backup
    ```
