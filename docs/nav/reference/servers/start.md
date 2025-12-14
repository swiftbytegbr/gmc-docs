# Start Server

Start a stopped server.

- Method: POST
- Path (REST): `/server/{serverId}/start`
- Returns: 204 No Content
- Backend behavior: Enqueues a start task. 409 if already running or busy.

=== "Java"

    ```java
    client.serverClient().startServer("srv-123").execute();
    ```

=== "JavaScript"

    ```ts
    await client.serverClient.startServer('srv-123');
    ```

=== "Python"

    ```python
    client.server_client.start_server('srv-123')
    ```

=== "REST"

    ```bash
    curl -X POST -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
      https://api.gamemanager.cloud/server/srv-123/start
    ```
