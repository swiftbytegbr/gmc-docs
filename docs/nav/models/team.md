# Model: Team

Represents your team and related members/application users.

Fields:
- `id` (string)
- `name` (string)
- `iconBase64` (string|null): Legacy inline icon representation
- `iconImageId` (string|null): Image id for icon served via `/images/{imageId}`
- `owner` (TeamMember)
- `members` (TeamMember[])
- `applications` (map<string, Permission[]>): Application users and their permissions
- `invitedMembers` (TeamInvite[]): Pending invites with metadata
- `inviteCode` (string)
- `limits` (Limits): Effective per-team limits

Nested: TeamMember
- `id`, `name`, `email`, `iconBase64`, `imageId`, `permissions` (Permission[]), `twoFAEnabled` (boolean)

Nested: TeamInvite
- `id`, `name`, `email`, `iconBase64`, `imageId`, `invitedAt` (ISO-8601), `expired` (boolean)

Nested: Limits
- `maxNodes`, `maxServers`, `maxBackups`, `maxRconCommands`, `maxStatisticsSize`, `maxMembers`

Example:
```json
{
  "id": "team-1",
  "name": "Dev Guild",
  "iconBase64": null,
  "iconImageId": "img-abc123",
  "owner": {
    "id": "u1",
    "name": "Alice",
    "email": "alice@example.com",
    "iconBase64": null,
    "imageId": "img-owner1",
    "permissions": ["ALL"],
    "twoFAEnabled": true
  },
  "members": [],
  "applications": { "app-1": ["MANAGE_SERVERS", "ACCESS_SERVERS"] },
  "invitedMembers": [
    {
      "id": "u2",
      "name": "Bob",
      "email": "bob@example.com",
      "iconBase64": null,
      "imageId": "img-invite1",
      "invitedAt": "2025-12-01T10:15:30Z",
      "expired": false
    }
  ],
  "inviteCode": "ABCD1234",
  "limits": {
    "maxNodes": 5,
    "maxServers": 10,
    "maxBackups": 20,
    "maxRconCommands": 1000,
    "maxStatisticsSize": 100,
    "maxMembers": 10
  }
}
```
