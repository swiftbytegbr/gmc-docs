# Update Server

Trigger a game server update (e.g., pull latest game build/mods depending on backend).

- Method: POST
- Path (REST): `/server/{serverId}/update`
- Returns: 200 OK
- Backend behavior: Triggers an update; the server may be stopped during update.

=== "Java"

    ```java
    client.serverClient().updateServer("srv-123").execute();
    ```

=== "JavaScript"

    ```ts
    await client.serverClient.updateServer('srv-123');
    ```

=== "Python"

    ```python
    client.server_client.update_server('srv-123')
    ```

=== "REST"

    ```bash
    curl -X POST -H "Application-Token: $GMC_APP_TOKEN" \
      https://api.gamemanager.cloud/server/srv-123/update
    ```
