# Get Server

Fetch a single server by ID.

- Method: GET
- Path (REST): `/server/{serverId}`
- Returns: GameServer
- Backend behavior: 404 if not within your team.

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

=== "Java"
```java
var srv = client.serverClient().getGameServer("srv-123").execute();
```

=== "JavaScript"
```ts
const srv = await client.serverClient.getGameServer('srv-123');
```

=== "Python"
```python
srv = client.server_client.get_game_server('srv-123')
```

=== "REST"
```bash
curl -s -H "Application-Token: $GMC_APP_TOKEN" \
  https://api.gamemanager.cloud/server/srv-123
```
