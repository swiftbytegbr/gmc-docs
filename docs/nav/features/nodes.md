# Nodes

Nodes represent your infrastructure: physical or virtual machines that host one or more game servers. GMC keeps track of each node’s identity, version, tasks and configurable settings. Most node operations are safe and read‑only, while a few (like update or settings changes) schedule work to be performed by the node agent.

When you query nodes, the backend filters to the scope of your team. When you change settings or trigger an update, the backend validates the request and offloads execution to the node. Tasks provide transparency into what the node is currently doing and what has completed recently.

## What you can do
You can discover your nodes, retrieve a single node’s details, trigger a software update on a node, update its settings (e.g., paths or resource limits), and review/abort long‑running tasks when supported.

## Java
```java
java.util.List<Node> nodes = client.nodeClient().getNodes().execute();
Node node = client.nodeClient().getNode("node-123").execute();
client.nodeClient().updateNode("node-123").execute();
client.nodeClient().changeSettings("node-123", new NodeSettings()).execute();
java.util.List<NodeTask> tasks = client.nodeClient().getNodeTasks("node-123").execute();
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
The REST endpoints for nodes are straightforward and read‑friendly. Mutating actions like update and cancel are POSTs to clearly indicate intent.

- List by team: `GET /node/by-team/{teamId}`
- Get by id: `GET /node/{nodeId}`
- Update: `POST /node/{nodeId}/update`
- Tasks: `GET /node/{nodeId}/task` / `GET /node/{nodeId}/task/{taskId}` / `POST /node/{nodeId}/task/{taskId}/cancel`
