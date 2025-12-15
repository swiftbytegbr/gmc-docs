# List Servers (by team)

List all servers for your team.

- Method: GET
- Path (REST): `/server/by-team/{teamId}`
- Returns: Array of GameServer
- Backend behavior: Team-scoped; read-only.

## Responses
- 200 OK: List of servers.
- 403 Forbidden: `missingPermission.ACCESS_SERVERS` — you lack read access in this team.
- 404 Not Found: `general.not_found` — team not found.

=== "Java"

    ```java
    java.util.List<GameServer> servers = gmc.serverClient().getGameServers().execute();
    ```

=== "JavaScript"

    ```ts
    const servers = await gmc.serverClient.getGameServers();
    ```

=== "Python"

    ```python
    servers = gmc.server_client.get_game_servers()
    ```

=== "REST"

    ```bash
    curl -s -H "Application-Token: $GMC_APP_TOKEN" \
      https://api.gamemanager.cloud/server/by-team/$TEAM_ID
    ```
