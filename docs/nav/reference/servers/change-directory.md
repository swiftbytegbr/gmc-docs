# Change Server Directory

Set a new directory path for the server's files.

- Method: POST
- Path (REST): `/server/{serverId}/change-directory`
- Body: `{ "serverDirectory": "/servers/cs2" }`
- Returns: 204 No Content
- Backend behavior: Creates a task to apply directory changes on the node; progress is tracked as a task. A restart may be required to take effect.

=== "Java"

    ```java
    client.serverClient().changeDirectory("srv-123", "/servers/cs2").execute();
    ```

=== "JavaScript"

    ```ts
    await client.serverClient.changeDirectory('srv-123', '/servers/cs2');
    ```

=== "Python"

    ```python
    client.server_client.change_directory('srv-123', '/servers/cs2')
    ```

=== "REST"

    ```bash
    curl -X POST -H "Content-Type: application/json" \
      -H "Application-Token: $GMC_APP_TOKEN" \
      -d '{"serverDirectory":"/servers/cs2"}' \
      https://api.gamemanager.cloud/server/srv-123/change-directory
    ```
