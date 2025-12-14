# Stop Server

Gracefully stop a running server.

- Method: POST
- Path (REST): `/server/{serverId}/stop`
- Returns: 204 No Content
- Backend behavior: Stops a running server. 409 if already stopping/stopped.

=== "Java"

    ```java
    client.serverClient().stopServer("srv-123").execute();
    ```

=== "JavaScript"

    ```ts
    await client.serverClient.stopServer('srv-123');
    ```

=== "Python"

    ```python
    client.server_client.stop_server('srv-123')
    ```

=== "REST"

    ```bash
    curl -X POST -H "Application-Token: $GMC_APP_TOKEN" \
      https://api.gamemanager.cloud/server/srv-123/stop
    ```
