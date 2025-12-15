# Stop Server

Gracefully stop a running server.

- Method: POST
- Path (REST): `/server/{serverId}/stop`
- Returns: 200 OK
- Backend behavior: Stops a running server. Supports optional delayed stop and force stop.

## Request body (optional)
- `forceStop` (boolean): Forcefully terminate the process; allowed when not OFFLINE.
- `delayMinutes` (int): Schedule a timed shutdown in N minutes.
- `delayedStopMessage` (string): Optional message broadcast before a scheduled stop.

## Responses
- 200 OK: Stop requested.
- 403 Forbidden: `missingPermission.MANAGE_SERVERS` — you lack the permission to manage servers in this team.
- 404 Not Found: `general.not_found` — server not found or not in your team.
- 400 Bad Request: `validation.failed` — invalid body (e.g., wrong types).
- 409 Conflict: `server.stop_normal_invalid_state` — graceful stop requires ONLINE.
- 409 Conflict: `server.stop_force_already_offline` — cannot force stop when already OFFLINE.
- 409 Conflict: `server.timed_shutdown_already_scheduled` — a timed stop/restart is already scheduled on this node for this server.
- 409 Conflict: `server.server_directory_change_in_progress` — a server directory change task is running on this server.

=== "Java"

    ```java
    gmc.serverClient().stopServer("srv-123").execute();
    ```

=== "JavaScript"

    ```ts
    await gmc.serverClient.stopServer('srv-123');
    ```

=== "Python"

    ```python
    gmc.server_client.stop_server('srv-123')
    ```

=== "REST"

    ```bash
    curl -X POST -H "Application-Token: $GMC_APP_TOKEN" \
      https://api.gamemanager.cloud/server/srv-123/stop
    ```
