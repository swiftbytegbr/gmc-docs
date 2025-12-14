# Change Node Settings

Apply configuration changes to a node.

- Method: POST
- Path (REST): `/node/{nodeId}/settings`
- Body: NodeSettings JSON
- Returns: 204 No Content
- Backend behavior: Validates and persists settings, may restart services depending on fields.

=== "Java"

    ```java
    NodeSettings settings = new NodeSettings();
    // settings.set...;
    client.nodeClient().changeSettings("node-123", settings).execute();
    ```

=== "JavaScript"

    ```ts
    await client.nodeClient.changeSettings('node-123', { /* fields */ });
    ```

=== "Python"

    ```python
    client.node_client.change_settings('node-123', { /* fields */ })
    ```

=== "REST"

    ```bash
    curl -X POST \
      -H "Content-Type: application/json" \
      -H "Application-Token: $GMC_APP_TOKEN" \
      -d '{"...":"..."}' \
      https://api.gamemanager.cloud/node/node-123/settings
    ```
