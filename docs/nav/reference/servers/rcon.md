# RCON Command

Send an RCON command to a running server.

- Method: POST
- Path (REST): `/server/{serverId}/rcon`
- Body: `{ "command": "status" }`
- Returns: 200 OK (output is delivered via RCON response stomp packet or can be retrieved from the server model)
- Backend behavior: Requires the server to be ONLINE and RCON configured.



=== "Java"

    ```java
    gmc.serverClient().rconCommand("srv-123", "status").execute();
    ```

=== "JavaScript"

    ```ts
    await gmc.serverClient.rconCommand('srv-123', 'status');
    ```

=== "Python"

    ```python
    gmc.server_client.rcon_command('srv-123', 'status')
    ```

=== "REST"

    ```bash
    curl -X POST -H "Content-Type: application/json" \
      -H "Application-Token: $GMC_APP_TOKEN" \
      -d '{"command":"status"}' \
      https://api.gamemanager.cloud/server/srv-123/rcon
    ```

## Responses
- 200 OK: RCON command sent.
- 403 Forbidden: `missingPermission.MANAGE_SERVERS` — you lack the permission to manage servers in this team.
- 404 Not Found: `general.not_found` — server not found or not in your team.
- 400 Bad Request: `validation.failed` — invalid command (blank or too long).
- 409 Conflict: `server.is_not_online` — RCON requires ONLINE.
- 409 Conflict: `server.server_directory_change_in_progress` — a server directory change task is running on this server.