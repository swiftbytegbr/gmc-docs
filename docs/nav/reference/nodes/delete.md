# Delete Node

Permanently delete a node. Use with care.

- Method: DELETE
- Path (REST): `/node/{nodeId}`
- Returns: 204 No Content
- Backend behavior: Deletes metadata; might require no active servers on the node. May return 409 if busy.

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
