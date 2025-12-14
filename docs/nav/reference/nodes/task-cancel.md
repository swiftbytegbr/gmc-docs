# Cancel Node Task

Cancel a cancellable task on a node.

- Method: POST
- Path (REST): `/node/{nodeId}/task/{taskId}/cancel`
- Returns: 200 OK
- Backend behavior: If task is not cancellable or already finished, backend returns 400/409.

=== "Java"

    ```java
    gmc.nodeClient().cancelNodeTask("node-123", "task-1").execute();
    ```

=== "JavaScript"

    ```ts
    await client.nodeClient.cancelNodeTask('node-123', 'task-1');
    ```

=== "Python"

    ```python
    client.node_client.cancel_node_task('node-123', 'task-1')
    ```

=== "REST"

    ```bash
    curl -X POST -H "Application-Token: $GMC_APP_TOKEN" \
      https://api.gamemanager.cloud/node/node-123/task/task-1/cancel
    ```
