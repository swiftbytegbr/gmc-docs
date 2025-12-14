# Get Notifications

Fetch notifications for your team. You can filter to only unread notifications using the `onlyUnread` flag.

- Method: GET
- Path (REST): `/team/{teamId}/notifications?onlyUnread=true|false`
- Returns: Array of Notification

### About `onlyUnread`
- `true`: returns only notifications that are currently marked as unread
- `false` (or omitted): returns all notifications (read and unread)
Use the unread count endpoint (`/team/{teamId}/notifications/unread-count`) when you just need a number without transferring the full list.

=== "Java"

    ```java
    java.util.List<Notification> notifications = gmc.teamClient().getNotifications(true).execute();
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
