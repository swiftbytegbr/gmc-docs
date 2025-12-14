# Get Max Players

Return the server's configured maximum player count.

- Method: GET
- Path (REST): `/server/{serverId}/maxPlayers`
- Returns: integer
- Backend behavior: Reads configuration from server metadata/config.

=== "Java"
```java
int maxPlayers = client.serverClient().getMaxPlayers("srv-123").execute();
```

=== "JavaScript"
```ts
const max = await client.serverClient.getMaxPlayers('srv-123');
```

=== "Python"
```python
max_players = client.server_client.get_max_players('srv-123')
```

=== "REST"
```bash
curl -s -H "Application-Token: $GMC_APP_TOKEN" \
  https://api.gamemanager.cloud/server/srv-123/maxPlayers
```
