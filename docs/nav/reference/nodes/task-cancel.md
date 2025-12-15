# Cancel Node Task

Cancel a cancellable task on a node.

- Method: POST
- Path (REST): `/node/{nodeId}/task/{taskId}/cancel`
- Returns: 202 Accepted
- Backend behavior: Requests cancellation for a cancellable task. If the task is not cancellable or already terminal, returns a conflict.

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

## Responses
- 202 Accepted: Cancellation requested.
- 403 Forbidden: `missingPermission.MANAGE_NODES` — you lack permission to manage nodes in this team.
- 404 Not Found: `general.not_found` — task or node not found.
- 409 Conflict: `node.task_not_cancelable` — task cannot be canceled.
- 400 Bad Request: `validation.failed` — invalid `nodeId` or `taskId` format.
