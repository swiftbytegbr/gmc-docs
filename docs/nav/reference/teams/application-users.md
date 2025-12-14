# Get Application Users

List application-user mappings for your team (apps with access to the team).

- Method: GET
- Path (REST): `/team/{teamId}/application-users`
- Returns: Array of ApplicationUser

=== "Java"

    ```java
    var users = client.teamClient().getApplicationUsers().execute();
    ```

=== "JavaScript"

    ```ts
    const users = await client.teamClient.getApplicationUsers();
    ```

=== "Python"

    ```python
    users = client.team_client.get_application_users()
    ```

=== "REST"

    ```bash
    curl -s -H "Application-Token: $GMC_APP_TOKEN" \
      https://api.gamemanager.cloud/team/$TEAM_ID/application-users
    ```
