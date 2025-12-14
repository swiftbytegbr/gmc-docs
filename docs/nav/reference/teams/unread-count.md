# Unread Notification Count

Return the number of unread notifications for your team.

- Method: GET
- Path (REST): `/team/{teamId}/notifications/unread-count`
- Returns: Number

=== "Java"
```java
long count = client.teamClient().getUnreadNotificationCount().execute();
```

=== "JavaScript"
```ts
const count = await client.teamClient.getUnreadNotificationCount();
```

=== "Python"
```python
count = client.team_client.get_unread_notification_count()
```

=== "REST"
```bash
curl -s -H "Application-Token: $GMC_APP_TOKEN" \
  https://api.gamemanager.cloud/team/$TEAM_ID/notifications/unread-count
```
