# Get Node Task

Fetch details of a single task on a node.

- Method: GET
- Path (REST): `/node/{nodeId}/task/{taskId}`
- Returns: NodeTask
- Backend behavior: Read-only.

=== "Java"

    ```java
    NodeTask task = client.nodeClient().getNodeTask("node-123", "task-1").execute();
    ```

=== "JavaScript"

    ```ts
    const task = await client.nodeClient.getNodeTask('node-123', 'task-1');
    ```

=== "Python"

    ```python
    task = client.node_client.get_node_task('node-123', 'task-1')
    ```

=== "REST"

    ```bash
    curl -s -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
      https://api.gamemanager.cloud/node/node-123/task/task-1
    ```

## Responses
- 200 OK: Task details returned.
- 403 Forbidden: `missingPermission.ACCESS_NODES` — you lack read access in this team.
- 404 Not Found: `general.not_found` — task or node not found.
- 400 Bad Request: `validation.failed` — invalid `nodeId` or `taskId` format.
