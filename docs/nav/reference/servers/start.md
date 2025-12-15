# Start Server

Start a stopped server.

- Method: POST
- Path (REST): `/server/{serverId}/start`
- Returns: 200 OK
- Backend behavior: Starts the server if the server is OFFLINE. The request returns immediately; the process continues asynchronously.

Note that this request completes immediately and does not wait for the server to be fully started.

=== "Java"

    ```java
    gmc.serverClient().startServer("srv-123").execute();
    ```

=== "JavaScript"

    ```ts
    await gmc.serverClient.startServer('srv-123');
    ```

=== "Python"

    ```python
    gmc.server_client.start_server('srv-123')
    ```

=== "REST"

    ```bash
    curl -X POST -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
      https://api.gamemanager.cloud/server/srv-123/start
    ```


## Responses
- 200 OK: Server start requested.
- 403 Forbidden: `missingPermission.MANAGE_SERVERS` — you lack the permission to manage servers in this team.
- 404 Not Found: `general.not_found` — server not found or not in your team.
- 409 Conflict: `server.is_not_offline` — the server must be OFFLINE to start.
- 409 Conflict: `server.server_directory_change_in_progress` — a server directory change task is running on this server.
