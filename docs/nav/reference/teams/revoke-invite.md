# Revoke Invite

Revoke a pending team invite by user ID.

- Method: DELETE
- Path (REST): `/team/{teamId}/invite/{userId}`
- Returns: 204 No Content

=== "Java"

    ```java
    client.teamClient().revokeInvite("user-123").execute();
    ```

=== "JavaScript"

    ```ts
    await client.teamClient.revokeInvite('user-123');
    ```

=== "Python"

    ```python
    client.team_client.revoke_invite('user-123')
    ```

=== "REST"

    ```bash
    curl -X DELETE -H "Application-Token: $GMC_APP_TOKEN" \
      https://api.gamemanager.cloud/team/$TEAM_ID/invite/user-123
    ```
