# List Servers (by team)

List all servers for your team.

- Method: GET
- Path (REST): `/server/by-team/{teamId}`
- Returns: Array of GameServer
- Backend behavior: Team-scoped; read-only.

=== "Java"

    ```java
    java.util.List<GameServer> servers = gmc.serverClient().getGameServers().execute();
    ```

=== "JavaScript"

    ```ts
    const servers = await client.serverClient.getGameServers();
    ```

=== "Python"

    ```python
    servers = client.server_client.get_game_servers()
    ```

=== "REST"

    ```bash
    curl -s -H "Application-Token: $GMC_APP_TOKEN" \
      https://api.gamemanager.cloud/server/by-team/$TEAM_ID
    ```
