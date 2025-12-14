# Delete Application User

Remove an application-user mapping by application ID.

- Method: DELETE
- Path (REST): `/team/{teamId}/application-user/{applicationId}`
- Returns: 200 OK

=== "Java"

    ```java
    client.teamClient().deleteApplicationUser("app-123").execute();
    ```

=== "JavaScript"

    ```ts
    await client.teamClient.deleteApplicationUser('app-123');
    ```

=== "Python"

    ```python
    client.team_client.delete_application_user('app-123')
    ```

=== "REST"

    ```bash
    curl -X DELETE -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
      https://api.gamemanager.cloud/team/$TEAM_ID/application-user/app-123
    ```
