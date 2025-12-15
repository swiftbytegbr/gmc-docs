# List Servers (by node)

List all servers hosted on a specific node.

- Method: GET
- Path (REST): `/server/by-node/{nodeId}`
- Returns: Array of GameServer
- Backend behavior: Read-only. Only servers your team owns are returned.


=== "Java"

    ```java
    java.util.List<GameServer> servers = gmc.serverClient().getGameServersByNode("node-123").execute();
    ```

=== "JavaScript"

    ```ts
    const servers = await gmc.serverClient.getGameServersByNode('node-123');
    ```

=== "Python"

    ```python
    servers = gmc.server_client.get_game_servers_by_node('node-123')
    ```

=== "REST"

    ```bash
    curl -s -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
      https://api.gamemanager.cloud/server/by-node/node-123
    ```

## Responses
- 200 OK: List of servers on the node.
- 403 Forbidden: `missingPermission.ACCESS_SERVERS` — you lack read access for the node’s team.
- 404 Not Found: `general.not_found` — node not found.