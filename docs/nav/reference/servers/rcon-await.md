Title: RCON Command (await)

Overview
- POST `/server/{serverId}/rcon?await=true[&timeoutMs=5000]`
- Sends an RCON command and waits for the daemon’s response (correlated via `commandId`). Returns the response payload with the command and its output.
- Use this when you need the response immediately (e.g., to show to a user, or to feed into automation logic on the client side).

When to use await vs non‑await
- Await: interactive tools, synchronous checks, or when you must display or process the output right away.
- Non‑await: fire‑and‑forget automations, bulk actions, or when output is handled elsewhere (e.g., via STOMP feed or logged on the server).

Permissions
- Requires `MANAGE_SERVERS` on the server’s team.

Request
- Path:
  - `serverId`: string (the server to run the command on)
- Query:
  - `await=true` (required to use this endpoint)
  - `timeoutMs`: optional integer; default ≈ 5000 ms. Controls how long the backend waits before returning a timeout error.
- Body (JSON):
  - `command`: string, the exact RCON command to run.

Response (200 OK)
```json
{
  "serverId": "srv_123",
  "command": {
    "command": "status",
    "response": "... server output ...",
    "commandId": "7f7c5a48-0d4a-4d2f-857d-1bbd1a71c9a0",
    "timestamp": "2025-01-01T12:00:00Z"
  }
}
```

Errors
- 409 Conflict: server is not ONLINE
- 408/400 with key `server.rcon_timeout`: response not received before `timeoutMs`
- Standard validation and permission errors may also apply.

Examples

=== "cURL"
```bash
curl -X POST \
  "https://api.gamemanager.cloud/server/srv_123/rcon?await=true&timeoutMs=7000" \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d '{"command":"status"}'
```

=== "JavaScript"
```ts
// Awaiting the response (SDK)
const res = await client.serverClient.rconCommandAwait("srv_123", "status", 7000);
console.log(res.command.response);

// Raw HTTP (fetch)
const r = await fetch(`/server/srv_123/rcon?await=true&timeoutMs=7000`, {
  method: 'POST',
  headers: { 'Content-Type': 'application/json', 'Authorization': `Bearer ${token}` },
  body: JSON.stringify({ command: 'status' })
});
if (!r.ok) throw new Error(await r.text());
const payload = await r.json();
```

=== "Java"
```java
// SDK usage
RconAwaitResponse res = client.serverClient()
    .rconCommandAwait("srv_123", "status", 7000L)
    .sync();
System.out.println(res.getCommand().getResponse());

// Raw HTTP (using HttpClient)
HttpRequest req = HttpRequest.newBuilder()
    .uri(URI.create(baseUrl + "/server/srv_123/rcon?await=true&timeoutMs=7000"))
    .header("Authorization", "Bearer " + token)
    .header("Content-Type", "application/json")
    .POST(BodyPublishers.ofString("{\"command\":\"status\"}"))
    .build();
HttpResponse<String> resp = http.send(req, BodyHandlers.ofString());
```

=== "Python"
```py
# SDK usage
res = client.server.rcon_command_await("srv_123", "status", timeout_ms=7000)
print(res["command"]["response"])  # dict payload

# Raw HTTP (requests)
import requests
r = requests.post(
    f"{base_url}/server/srv_123/rcon",
    params={"await": "true", "timeoutMs": 7000},
    headers={"Authorization": f"Bearer {token}"},
    json={"command": "status"}
)
r.raise_for_status()
payload = r.json()
```

Behavior and correlation
- The backend attaches a unique `commandId` to the RCON request (`RconCommand.commandId`) and waits for the daemon to echo it back in the response.
- If the daemon does not respond before `timeoutMs`, the backend returns an error with key `server.rcon_timeout`.
- Regardless of awaiting, responses are persisted and broadcast to the team via STOMP.

Best practices
- Keep `timeoutMs` modest (e.g., 3–7s) and retry on `server.rcon_timeout` if appropriate.
- Prefer non‑await for bulk operations or when you don’t need the output immediately to avoid tying up callers.
- For repeated queries (e.g., `status`), consider caching or rate limiting on the caller side.
