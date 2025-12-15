# Delete Node

Permanently delete a node. Use with care.

- Method: DELETE
- Path (REST): `/node/{nodeId}`
- Returns: 204 No Content
- Backend behavior: Deletes the node and fails/removes its tasks. Associated servers are force-deleted by the backend.

=== "Java"

    ```java
    client.nodeClient().deleteNode("node-123").execute();
    ```

=== "JavaScript"

    ```ts
    await client.nodeClient.deleteNode('node-123');
    ```

=== "Python"

    ```python
    client.node_client.delete_node('node-123')
    ```

=== "REST"

    ```bash
    curl -X DELETE \
      -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
      https://api.gamemanager.cloud/node/node-123
    ```

## Responses
- 204 No Content: Node deleted.
- 403 Forbidden: `missingPermission.MANAGE_NODES` — you lack permission to manage nodes in this team.
- 404 Not Found: `general.not_found` — node or team not found.
