# Kick Member

Remove a user from your team.

- Method: POST
- Path (REST): `/team/{teamId}/kick`
- Body: `{ "memberId": "user-123" }`
- Returns: 200 OK
- Backend behavior: Removes membership. Some permissions may be revoked immediately from running sessions.

=== "Java"

    ```java
    client.teamClient().kickMember("user-123").execute();
    ```

=== "JavaScript"

    ```ts
    await client.teamClient.kickMember('user-123');
    ```

=== "Python"

    ```python
    client.team_client.kick_member('user-123')
    ```

=== "REST"

    ```bash
    curl -X POST -H "Content-Type: application/json" \
      -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
      -d '{"memberId":"user-123"}' \
      https://api.gamemanager.cloud/team/$TEAM_ID/kick
    ```
