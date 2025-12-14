# Get Notifications

Fetch team notifications; optionally filter unread only.

- Method: GET
- Path (REST): `/team/{teamId}/notifications?onlyUnread=true|false`
- Returns: Array of Notification

=== "Java"

    ```java
    var notifications = client.teamClient().getNotifications(true).execute();
    ```

=== "JavaScript"

    ```ts
    const notifications = await client.teamClient.getNotifications(true);
    ```

=== "Python"

    ```python
    notifications = client.team_client.get_notifications(only_unread=True)
    ```

=== "REST"

    ```bash
    curl -s -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
      "https://api.gamemanager.cloud/team/$TEAM_ID/notifications?onlyUnread=true"
    ```
