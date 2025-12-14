# Get Node

Fetch a single node by ID.

- Method: GET
- Path (REST): `/node/{nodeId}`
- Returns: Node
- Backend behavior: Only nodes from your team are visible; otherwise 404. No side effects.

## Response
Example:
```json
{
  "id": "node-123",
  "teamId": "team-1",
  "inviteToken": 123456,
  "daemonVersion": "1.5.2",
  "lastAlive": "2025-01-01T12:34:56Z",
  "lastLogin": "2025-01-01T12:30:00Z",
  "logoutReason": null,
  "status": "ONLINE",
  "settings": {},
  "systemData": {}
}
```

=== "Java"

    ```java
    Node node = client.nodeClient().getNode("node-123").execute();
    ```

=== "JavaScript"

    ```ts
    const node = await client.nodeClient.getNode('node-123');
    ```

=== "Python"

    ```python
    node = client.node_client.get_node('node-123')
    ```

=== "REST"

    ```bash
    curl -s \
      -H "Accept: application/json" \
      -H "Application-Token: $GMC_APP_TOKEN" \
      https://api.gamemanager.cloud/node/node-123
    ```
