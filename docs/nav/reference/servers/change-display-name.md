# Change Display Name

Set a human-friendly display name for a server.

- Method: POST
- Path (REST): `/server/{serverId}/change-display-name`
- Body: `{ "displayName": "Public #1" }`
- Returns: 204 No Content
- Backend behavior: Metadata only; no restart required.

=== "Java"

    ```java
    client.serverClient().changeDisplayName("srv-123", "Public #1").execute();
    ```

=== "JavaScript"

    ```ts
    await client.serverClient.changeDisplayName('srv-123', 'Public #1');
    ```

=== "Python"

    ```python
    client.server_client.change_display_name('srv-123', 'Public #1')
    ```

=== "REST"

    ```bash
    curl -X POST -H "Content-Type: application/json" \
      -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
      -d '{"displayName":"Public #1"}' \
      https://api.gamemanager.cloud/server/srv-123/change-display-name
    ```
