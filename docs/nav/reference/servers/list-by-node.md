# List Servers (by node)

List all servers hosted on a specific node.

- Method: GET
- Path (REST): `/server/by-node/{nodeId}`
- Returns: Array of GameServer
- Backend behavior: Read-only. Only servers your team owns are returned.

=== "Java"

    ```java
    java.util.List<GameServer> servers = client.serverClient().getGameServersByNode("node-123").execute();
    ```

=== "JavaScript"

    ```ts
    const servers = await client.serverClient.getGameServersByNode('node-123');
    ```

=== "Python"

    ```python
    servers = client.server_client.get_game_servers_by_node('node-123')
    ```

=== "REST"

    ```bash
    curl -s -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
      https://api.gamemanager.cloud/server/by-node/node-123
    ```
