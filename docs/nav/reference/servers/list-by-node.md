# List Servers (by node)

List all servers hosted on a specific node.

- Method: GET
- Path (REST): `/server/by-node/{nodeId}`
- Returns: Array of GameServer
- Backend behavior: Read-only. Only servers your team owns are returned.


=== "Java"

    ```java
    java.util.List<GameServer> servers = gmc.serverClient().getGameServersByNode("node-123").execute();
    ```

=== "JavaScript"

    ```ts
    const servers = await gmc.serverClient.getGameServersByNode('node-123');
    ```

=== "Python"

    ```python
    servers = gmc.server_client.get_game_servers_by_node('node-123')
    ```

=== "REST"

    ```bash
    curl -s -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
      https://api.gamemanager.cloud/server/by-node/node-123
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
- 200 OK: List of servers on the node.
- 403 Forbidden: `missingPermission.ACCESS_SERVERS` — you lack read access for the node’s team.
- 404 Not Found: `general.not_found` — node not found.
