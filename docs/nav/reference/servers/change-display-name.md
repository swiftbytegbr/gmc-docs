# Change Display Name

Set a human-friendly display name for a server.

- Method: POST
- Path (REST): `/server/{serverId}/change-display-name`
- Body: `{ "displayName": "Public #1" }`
- Returns: 204 No Content
- Backend behavior: Metadata only; no restart required.


=== "Java"

    ```java
    gmc.serverClient().changeDisplayName("srv-123", "Public #1").execute();
    ```

=== "JavaScript"

    ```ts
    await gmc.serverClient.changeDisplayName('srv-123', 'Public #1');
    ```

=== "Python"

    ```python
    gmc.server_client.change_display_name('srv-123', 'Public #1')
    ```

=== "REST"

    ```bash
    curl -X POST -H "Content-Type: application/json" \
      -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
      -d '{"displayName":"Public #1"}' \
      https://api.gamemanager.cloud/server/srv-123/change-display-name
    ```

## Responses
- 204 No Content: Name updated.
- 403 Forbidden: `missingPermission.MANAGE_SERVERS` — you lack the permission to manage servers in this team.
- 404 Not Found: `general.not_found` — server not found or not in your team.
- 400 Bad Request: `validation.failed` — invalid display name.
- 409 Conflict: `server.display_name_already_exists` — name already in use within the team.
