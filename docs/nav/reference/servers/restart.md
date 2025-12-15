# Restart Server

Restart a server (stop then start).

- Method: POST
- Path (REST): `/server/{serverId}/restart`
- Returns: 200 OK
- Backend behavior: Performs a restart (requires server to be ONLINE). Optional delayed restart.

## Request body (optional)
- `delayMinutes` (int): Schedule a timed restart in N minutes.
- `delayedRestartMessage` (string): Optional message broadcast before a scheduled restart.


=== "Java"

    ```java
    gmc.serverClient().restartServer("srv-123").execute();
    ```

=== "JavaScript"

    ```ts
    await gmc.serverClient.restartServer('srv-123');
    ```

=== "Python"

    ```python
    gmc.server_client.restart_server('srv-123')
    ```

=== "REST"

    ```bash
    curl -X POST -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
      https://api.gamemanager.cloud/server/srv-123/restart
    ```

## Responses
- 200 OK: Restart requested.
- 403 Forbidden: `missingPermission.MANAGE_SERVERS` — you lack the permission to manage servers in this team.
- 404 Not Found: `general.not_found` — server not found or not in your team.
- 400 Bad Request: `validation.failed` — invalid body (e.g., wrong types).
- 409 Conflict: `server.is_not_online` — restart requires ONLINE.
- 409 Conflict: `server.timed_restart_already_scheduled` — a timed stop/restart is already scheduled on this node for this server.
- 409 Conflict: `server.server_directory_change_in_progress` — a server directory change task is running on this server.
