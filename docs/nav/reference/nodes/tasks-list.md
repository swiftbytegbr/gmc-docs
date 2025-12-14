# List Node Tasks

List tasks scheduled or in-progress on a node.

- Method: GET
- Path (REST): `/node/{nodeId}/task`
- Returns: Array of NodeTask
- Backend behavior: Includes running and history (depending on retention). Safe and read-only.

=== "Java"

    ```java
    java.util.List<NodeTask> tasks = client.nodeClient().getNodeTasks("node-123").execute();
    ```

=== "JavaScript"

    ```ts
    const tasks = await client.nodeClient.getNodeTasks('node-123');
    ```

=== "Python"

    ```python
    tasks = client.node_client.get_node_tasks('node-123')
    ```

=== "REST"

    ```bash
    curl -s -H "Application-Token: $GMC_APP_TOKEN" \
      https://api.gamemanager.cloud/node/node-123/task
    ```
