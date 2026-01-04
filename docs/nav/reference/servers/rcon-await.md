Title: RCON Command (await)

Endpoint
- POST `/server/{serverId}/rcon?await=true[&timeoutMs=5000]`

Description
- Sends an RCON command and waits for the daemon’s response, correlated by commandId. Returns the response packet.

Permissions
- `MANAGE_SERVERS` on the server’s team.

Request
- Path: `serverId` (string)
- Query:
  - `await=true` (required)
  - `timeoutMs` (optional, defaults to ~5000ms)
- Body (JSON):
  - `command` (string): RCON command to execute

Response (200 OK)
```
{
  "serverId": "...",
  "command": {
    "command": "status",
    "response": "...",
    "commandId": "uuid",
    "timestamp": "ISO-8601"
  }
}
```

Errors
- 409 Conflict: server is not ONLINE
- 408/400: `server.rcon_timeout` if the response did not arrive in time

SDK Usage
- JavaScript
  - `const res = await client.serverClient.rconCommandAwait(serverId, 'status', 5000)`
- Java
  - `RconAwaitResponse res = serverClient.rconCommandAwait(serverId, "status", 5000L).sync()`
- Python
  - `res = client.server.rcon_command_await(server_id, 'status', timeout_ms=5000)`

Notes
- Use non-await variant when you do not need the response synchronously.
