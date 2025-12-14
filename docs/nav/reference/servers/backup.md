# Backup Server

Create a named backup of a server.

- Method: POST
- Path (REST): `/server/{serverId}/backup`
- Body: `{ "name": "<backup-name>" }`
- Returns: 200 OK
- Backend behavior: Snapshot of files; may be async with a task; size and time depend on server contents.

=== "Java"

    ```java
    gmc.serverClient().backupServer("srv-123", "pre-update").execute();
    ```

=== "JavaScript"

    ```ts
    await client.serverClient.backupServer('srv-123', 'pre-update');
    ```

=== "Python"

    ```python
    client.server_client.backup_server('srv-123', 'pre-update')
    ```

=== "REST"

    ```bash
    curl -X POST -H "Content-Type: application/json" \
      -H "Application-Token: $GMC_APP_TOKEN" \
      -d '{"name":"pre-update"}' \
      https://api.gamemanager.cloud/server/srv-123/backup
    ```
