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

## Response
Example:
```json
[
  {
    "id": "srv-123",
    "displayName": "Public #1",
    "nodeId": "node-123",
    "created": "2025-01-01T12:00:00Z",
    "gameType": "ARK_ASCENDED",
    "state": "RUNNING",
    "settingProfileId": "prof-1",
    "serverDirectory": "/servers/ark",
    "onlinePlayers": 12,
    "backups": [],
    "commands": [],
    "nodeName": "eu-west-1",
    "serverIp": "203.0.113.12",
    "map": "Fjordur",
    "maxPlayers": 64,
    "modCount": 0,
    "serverPort": 27015,
    "queryPort": 27016,
    "rconPort": 27017
  }
]
```

## Responses
- 200 OK: List of servers.
- 403 Forbidden: `missingPermission.ACCESS_SERVERS` — you lack read access in this team.
- 404 Not Found: `general.not_found` — team not found.
