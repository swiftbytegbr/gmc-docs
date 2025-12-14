# Teams

Teams scope credentials, members, notifications, and action logs.

## What you can do
- Fetch your team and application users
- Invite/kick members and change permissions
- Upload a team icon (multipart)
- View notifications and unread counts
- View action log and revoke invites/application users

## Java
```java
var team = client.teamClient().getTeam();
client.teamClient().inviteMember("dev@example.com").execute();
client.teamClient().kickMember("user-123").execute();
client.teamClient().changeMemberPermission("user-123", List.of(Permission.ADMIN)).execute();
client.teamClient().changeTeamIcon(Files.readAllBytes(Path.of("icon.png")), "icon.png").execute();
var page = client.teamClient().getActionLog(0, 25).execute();
var users = client.teamClient().getApplicationUsers().execute();
client.teamClient().revokeInvite("user-123").execute();
client.teamClient().deleteApplicationUser("app-123").execute();
var notifications = client.teamClient().getNotifications(true).execute();
long unread = client.teamClient().getUnreadNotificationCount().execute();
```

## JavaScript
```ts
const team = await client.teamClient.getTeam();
await client.teamClient.inviteMember('dev@example.com');
await client.teamClient.kickMember('user-123');
await client.teamClient.setPermission('user-123', ['ADMIN']);
const notifications = await client.teamClient.getNotifications(true);
const unread = await client.teamClient.getUnreadNotificationCount();
```

## Python
```python
team = client.team_client.get_team()
client.team_client.invite_member('dev@example.com')
client.team_client.kick_member('user-123')
client.team_client.set_permission('user-123', ['ADMIN'])
notifications = client.team_client.get_notifications(only_unread=True)
unread = client.team_client.get_unread_notification_count()
```

## REST
- Get my team: `GET /team/my`
- Invite: `POST /team/{teamId}/invite`
- Kick: `POST /team/{teamId}/kick`
- Permissions: `POST /team/{teamId}/permission`
- Icon upload: `POST /team/{teamId}/icon` (multipart)
- Notifications: `GET /team/{teamId}/notifications` and `GET /team/{teamId}/notifications/unread-count`
- Action log: `GET /team/{teamId}/action-log`

