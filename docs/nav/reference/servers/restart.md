# Restart Server

Restart a server (stop then start).

- Method: POST
- Path (REST): `/server/{serverId}/restart`
- Returns: 204 No Content
- Backend behavior: Enqueues a restart task. 409 if busy.

=== "Java"
```java
client.serverClient().restartServer("srv-123").execute();
```

=== "JavaScript"
```ts
await client.serverClient.restartServer('srv-123');
```

=== "Python"
```python
client.server_client.restart_server('srv-123')
```

=== "REST"
```bash
curl -X POST -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
  https://api.gamemanager.cloud/server/srv-123/restart
```
