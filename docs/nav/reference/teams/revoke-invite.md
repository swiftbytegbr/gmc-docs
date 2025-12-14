# Revoke Invite

Revoke a pending team invite by user ID.

- Method: DELETE
- Path (REST): `/team/{teamId}/invite/{userEmail}`
- Returns: 200 OK

=== "Java"

    ```java
    client.teamClient().revokeInvite("test@domain.com").execute();
    ```

=== "JavaScript"

    ```ts
    await client.teamClient.revokeInvite('test@domain.com');
    ```

=== "Python"

    ```python
    client.team_client.revoke_invite('test@domain.com')
    ```

=== "REST"

    ```bash
    curl -X DELETE -H "Application-Token: $GMC_APP_TOKEN" \
      https://api.gamemanager.cloud/team/$TEAM_ID/invite/test@domain.com
    ```
