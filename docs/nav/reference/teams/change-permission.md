# Change Member Permission

Set a member's permissions within the team.

- Method: POST
- Path (REST): `/team/{teamId}/permission`
- Body: `{ "memberId": "user-123", "newPermissions": ["ADMIN"] }`
- Returns: 200 OK
- Backend behavior: Effective immediately for future actions; running tasks may continue.

=== "Java"

    ```java
    gmc.teamClient().changeMemberPermission("user-123", java.util.List.of(Permission.MANAGE_SERVERS)).execute();
    ```

=== "JavaScript"

    ```ts
    await client.teamClient.setPermission('user-123', ['ADMIN']);
    ```

=== "Python"

    ```python
    client.team_client.set_permission('user-123', ['ADMIN'])
    ```

=== "REST"

    ```bash
    curl -X POST -H "Content-Type: application/json" \
      -H "Application-Token: $GMC_APP_TOKEN" \
      -d '{"memberId":"user-123","newPermissions":["ADMIN"]}' \
      https://api.gamemanager.cloud/team/$TEAM_ID/permission
    ```
