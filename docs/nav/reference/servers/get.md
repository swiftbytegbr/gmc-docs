# Get Server

Fetch a single server by ID.

- Method: GET
- Path (REST): `/server/{serverId}`
- Returns: GameServer
- Backend behavior: Returns an enriched server view (ports, IPs, limits). Requires access to the team.

=== "Java"

    ```java
    GameServer srv = gmc.serverClient().getGameServer("srv-123").execute();
    ```

=== "JavaScript"

    ```ts
    const srv = await gmc.serverClient.getGameServer('srv-123');
    ```

=== "Python"

    ```python
    srv = gmc.server_client.get_game_server('srv-123')
    ```

=== "REST"

    ```bash
    curl -s -H "Application-Token: $GMC_APP_TOKEN" \
      https://api.gamemanager.cloud/server/srv-123
    ```

## Response
Example:
```json
{
  "id": "srv-123",
  "displayName": "Public #1",
  "nodeId": "node-123",
  "created": "2025-01-01T12:00:00Z",
  "version": "v1.0",
  "gameType": "ARK_ASCENDED",
  "state": "RUNNING",
  "settingProfileId": "prof-1",
  "serverDirectory": "/servers/ark",
  "onlinePlayers": 12,
  "nodeName": "eu-west-1",
  "serverIp": "203.0.113.12",
  "map": "Fjordur",
  "maxPlayers": 64,
  "modCount": 0,
  "serverPort": 27015,
  "queryPort": 27016,
  "rconPort": 27017
}
```

## Responses
- 200 OK: Server returned.
- 403 Forbidden: `missingPermission.ACCESS_SERVERS` — you lack read access in this team.
- 404 Not Found: `general.not_found` — server/node/team not found.
- 400 Bad Request: `server.unsupported_game_type` — unknown or unsupported game type for this server.
- 500 Internal Server Error: `server.dto_mapping_profile_not_found` — server’s setting profile is missing.
