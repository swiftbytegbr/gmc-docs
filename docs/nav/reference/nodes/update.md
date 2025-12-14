# Update Node

Trigger a node self-update. Typically pulls and applies the latest node software matching the backend versioning.

- Method: POST
- Path (REST): `/node/{nodeId}/update`
- Returns: 204 No Content
- Backend behavior: Enqueues an update task on the node. Idempotent; repeated calls re-trigger check.

=== "Java"
```java
client.nodeClient().updateNode("node-123").execute();
```

=== "JavaScript"
```ts
await client.nodeClient.updateNode('node-123');
```

=== "Python"
```python
client.node_client.update_node('node-123')
```

=== "REST"
```bash
curl -X POST \
  -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
  https://api.gamemanager.cloud/node/node-123/update
```
