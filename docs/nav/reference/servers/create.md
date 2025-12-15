# Create Server

Create a new game server on a node.

- Method: POST
- Path (REST): `/server/create`
- Body: `{ "nodeId": "node-123", "name": "My Server", "gameType": "CS2", "map": "de_dust2", "serverDirectory": "/servers/cs2", "enablePreaquaticaBeta": false }`
- Returns: GameServer
- Backend behavior: Allocates resources on the node, prepares files, and registers the server. Returns immediately; installation proceeds on the node.

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
  "teamId": "team-1",
  "nodeId": "node-123",
  "created": "2025-01-02T10:00:00Z",
  "gameType": "CS2",
  "state": "STOPPED",
  "settingProfileId": "prof-1",
  "serverDirectory": "/servers/cs2",
  "onlinePlayers": 0,
  "backups": [],
  "commands": []
}
```

=== "Java"

    ```java
    GameServer created = gmc.serverClient()
        .createServer("node-123", "My Server", GameType.CS2, "de_dust2", "/servers/cs2")
        .execute();
    ```

=== "JavaScript"

    ```ts
    const srv = await gmc.serverClient.createServer('node-123', 'My Server', 'CS2', 'de_dust2', '/servers/cs2');
    ```

=== "Python"

    ```python
    srv = gmc.server_client.create_server('node-123', 'My Server', 'CS2', 'de_dust2', '/servers/cs2')
    ```

=== "REST"

    ```bash
    curl -X POST -H "Content-Type: application/json" \
      -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
      -d '{"nodeId":"node-123","name":"My Server","gameType":"CS2","map":"de_dust2","serverDirectory":"/servers/cs2"}' \
      https://api.gamemanager.cloud/server/create
    ```

## Responses
- 200 OK: Server creation requested; returns the created server record.
- 403 Forbidden: `missingPermission.MANAGE_SERVERS` — you lack the permission to manage servers in this team.
- 404 Not Found: `general.not_found` — node not found or not in your team.
- 400 Bad Request: `validation.failed` — invalid `name` or body fields.
- 400 Bad Request: `server.unsupported_game_type` — unknown or unsupported game type.
- 400 Bad Request: `server.directory_required` — no directory provided and no node default configured.
- 409 Conflict: `server.display_name_already_exists` — display name already exists in this team.
- 409 Conflict: `team.too_many_servers` — team reached the maximum number of servers.
- 409 Conflict: `server.node_is_offline` — cannot create on an offline node.
