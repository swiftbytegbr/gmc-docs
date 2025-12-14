# Rollback Server

Roll a server back to a backup. Optionally restore player-related data.

- Method: POST
- Path (REST): `/server/{serverId}/rollback`
- Body: `{ "backupId": "<id>", "rollbackPlayers": true }`
- Returns: 204 No Content
- Backend behavior: Replaces server files from backup; downtime expected.

=== "Java"

    ```java
    client.serverClient().rollbackServer("srv-123", "backup-1", true).execute();
    ```

=== "JavaScript"

    ```ts
    await client.serverClient.rollbackServer('srv-123', 'backup-1', true);
    ```

=== "Python"

    ```python
    client.server_client.rollback_server('srv-123', 'backup-1', True)
    ```

=== "REST"

    ```bash
    curl -X POST -H "Content-Type: application/json" \
      -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
      -d '{"backupId":"backup-1","rollbackPlayers":true}' \
      https://api.gamemanager.cloud/server/srv-123/rollback
    ```
