# Create Server

Create a new game server on a node.

- Method: POST
- Path (REST): `/server/create`
- Body: `{ "nodeId": "node-123", "name": "My Server", "gameType": "CS2", "map": "de_dust2", "serverDirectory": "/servers/cs2", "enablePreaquaticaBeta": false }`
- Returns: GameServer
- Backend behavior: Allocates resources on the node, prepares files, and registers the server. May take time.

## Request body
```json
{
  "nodeId": "node-123",
  "name": "My Server",
  "gameType": "CS2",
  "map": "de_dust2",
  "serverDirectory": "/servers/cs2",
  "enablePreaquaticaBeta": false
}
```

## Response
Returns a `GameServer` object. Example:
```json
{
  "id": "srv-abc",
  "displayName": "My Server",
  "nodeId": "node-123",
  "created": "2025-01-02T10:00:00Z",
  "version": "v1.0",
  "gameType": "CS2",
  "state": "STOPPED",
  "settingProfileId": "prof-1",
  "serverDirectory": "/servers/cs2",
  "onlinePlayers": 0
}
```

=== "Java"
```java
var created = client.serverClient()
  .createServer("node-123", "My Server", GameType.CS2, "de_dust2", "/servers/cs2")
  .execute();
```

=== "JavaScript"
```ts
const srv = await client.serverClient.createServer('node-123', 'My Server', 'CS2', 'de_dust2', '/servers/cs2');
```

=== "Python"
```python
srv = client.server_client.create_server('node-123', 'My Server', 'CS2', 'de_dust2', '/servers/cs2')
```

=== "REST"
```bash
curl -X POST -H "Content-Type: application/json" \
  -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
  -d '{"nodeId":"node-123","name":"My Server","gameType":"CS2","map":"de_dust2","serverDirectory":"/servers/cs2"}' \
  https://api.gamemanager.cloud/server/create
```
