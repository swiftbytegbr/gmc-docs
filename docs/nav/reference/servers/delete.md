# Delete Server

Permanently delete a server.

- Method: POST
- Path (REST): `/server/{serverId}/delete`
- Body: `{ "forceDelete": false }`
- Returns: 204 No Content
- Backend behavior: 409 if server is running; use `forceDelete: true` to override if supported by policy.

=== "Java"

    ```java
    client.serverClient().deleteServer("srv-123", false).execute();
    ```

=== "JavaScript"

    ```ts
    await client.serverClient.deleteServer('srv-123', false);
    ```

=== "Python"

    ```python
    client.server_client.delete_server('srv-123', False)
    ```

=== "REST"

    ```bash
    curl -X POST -H "Content-Type: application/json" \
      -H "Application-Token: $GMC_APP_TOKEN" \
      -d '{"forceDelete":false}' \
      https://api.gamemanager.cloud/server/srv-123/delete
    ```
