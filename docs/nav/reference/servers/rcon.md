# RCON Command

Send an RCON command to a running server.

- Method: POST
- Path (REST): `/server/{serverId}/rcon`
- Body: `{ "command": "status" }`
- Returns: 204 No Content (output may be surfaced through logs/statistics)
- Backend behavior: Requires RCON enabled and configured.

=== "Java"
```java
client.serverClient().rconCommand("srv-123", "status").execute();
```

=== "JavaScript"
```ts
await client.serverClient.rconCommand('srv-123', 'status');
```

=== "Python"
```python
client.server_client.rcon_command('srv-123', 'status')
```

=== "REST"
```bash
curl -X POST -H "Content-Type: application/json" \
  -H "Application-Token: $GMC_APP_TOKEN" \
  -d '{"command":"status"}' \
  https://api.gamemanager.cloud/server/srv-123/rcon
```
