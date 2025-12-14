# Nodes

Nodes represent machines hosting game servers.

## What you can do
- List nodes for your team
- Get a specific node
- Update a node
- Change node settings
- Inspect/cancel node tasks

## Java
```java
var nodes = client.nodeClient().getNodes().execute();
var node = client.nodeClient().getNode("node-123").execute();
client.nodeClient().updateNode("node-123").execute();
client.nodeClient().changeSettings("node-123", new NodeSettings()).execute();
var tasks = client.nodeClient().getNodeTasks("node-123").execute();
```

## JavaScript
```ts
const nodes = await client.nodeClient.getNodes();
const node = await client.nodeClient.getNode('node-123');
await client.nodeClient.updateNode('node-123');
```

## Python
```python
nodes = client.node_client.get_nodes()
node = client.node_client.get_node('node-123')
client.node_client.update_node('node-123')
```

## REST
- List by team: `GET /node/by-team/{teamId}`
- Get by id: `GET /node/{nodeId}`
- Update: `POST /node/{nodeId}/update`
- Tasks: `GET /node/{nodeId}/task` / `GET /node/{nodeId}/task/{taskId}` / `POST /node/{nodeId}/task/{taskId}/cancel`

