# Get Server

Fetch a single server by ID.

- Method: GET
- Path (REST): `/server/{serverId}`
- Returns: GameServer
- Backend behavior: 404 if not within your team.

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
