# Change Node Settings

Apply configuration changes to a node.

- Method: POST
- Path (REST): `/node/{nodeId}/settings`
- Body: NodeSettings JSON
- Returns: 204 No Content
- Backend behavior: Validates and persists settings. Fails if node is not ONLINE or a backup directory change task is active.

=== "Java"

    ```java
    NodeSettings settings = new NodeSettings();
    // settings.set...;
    client.nodeClient().changeSettings("node-123", settings).execute();
    ```

=== "JavaScript"

    ```ts
    await client.nodeClient.changeSettings('node-123', { /* fields */ });
    ```

=== "Python"

    ```python
    client.node_client.change_settings('node-123', { /* fields */ })
    ```

=== "REST"

    ```bash
    curl -X POST \
      -H "Content-Type: application/json" \
      -H "Application-Token: $GMC_APP_TOKEN" \
      -d '{"...":"..."}' \
      https://api.gamemanager.cloud/node/node-123/settings
    ```

## Responses
- 204 No Content: Settings updated.
- 403 Forbidden: `missingPermission.MANAGE_NODES` — you lack permission to manage nodes in this team.
- 404 Not Found: `general.not_found` — node or team not found.
- 400 Bad Request: `validation.failed` — invalid body or path parameter.
- 409 Conflict: `node.invalid_state` — node must be ONLINE to change settings.
- 409 Conflict: `node.backup_directory_change_in_progress` — cannot change settings while the node is changing the backups directory.
