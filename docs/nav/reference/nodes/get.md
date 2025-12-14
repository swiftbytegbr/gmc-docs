# Get Node

Fetch a single node by ID.

- Method: GET
- Path (REST): `/node/{nodeId}`
- Returns: Node
- Backend behavior: Only nodes from your team are visible; otherwise 404. No side effects.

=== "Java"
```java
var node = client.nodeClient().getNode("node-123").execute();
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
