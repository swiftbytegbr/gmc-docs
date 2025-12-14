# Invite Member

Invite a user to your team by email.

- Method: POST
- Path (REST): `/team/{teamId}/invite`
- Body: `{ "userEmail": "dev@example.com" }`
- Returns: 204 No Content
- Backend behavior: Creates a pending invite for the email. May send notification.

=== "Java"

    ```java
    client.teamClient().inviteMember("dev@example.com").execute();
    ```

=== "JavaScript"

    ```ts
    await client.teamClient.inviteMember('dev@example.com');
    ```

=== "Python"

    ```python
    client.team_client.invite_member('dev@example.com')
    ```

=== "REST"

    ```bash
    curl -X POST -H "Content-Type: application/json" \
      -H "Application-Token: $GMC_APP_TOKEN" \
      -d '{"userEmail":"dev@example.com"}' \
      https://api.gamemanager.cloud/team/$TEAM_ID/invite
    ```
