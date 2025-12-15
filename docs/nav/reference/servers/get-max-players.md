# Get Max Players

Return the maximum number of players supported by the server’s current configuration.

- Method: GET
- Path (REST): `/server/{serverId}/maxPlayers`
- Returns: integer (e.g., `64`)
- Backend behavior: Derived from the server’s setting profile and game handler.

## Responses
- 200 OK: Max players value returned.
- 403 Forbidden: `missingPermission.ACCESS_SERVERS` — you lack read access in this team.
- 404 Not Found: `general.not_found` — server not found or not in your team.
- 400 Bad Request: `server.unsupported_game_type` — no handler for the server’s game type.

=== "Java"

```java
int max = gmc.serverClient().getMaxPlayers("srv-123").execute();
```

=== "JavaScript"

```ts
const max = await gmc.serverClient.getMaxPlayers('srv-123');
```

=== "Python"

```python
max_players = gmc.server_client.get_max_players('srv-123')
```

=== "REST"

```bash
curl -s -H "Application-Token: $GMC_APP_TOKEN" \
  https://api.gamemanager.cloud/server/srv-123/maxPlayers
```

