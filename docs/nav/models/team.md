# Model: Team

Represents your team and related members/application users.

Fields:
- `id` (string)
- `name` (string)
- `iconBase64` (string|null): Inline icon representation
- `owner` (TeamMember)
- `members` (TeamMember[])
- `applications` (map<string, Permission[]>): Application users and their permissions
- `invitedMembers` (string[]): Pending invites (emails or IDs)
- `inviteCode` (string)
- `actionLog` (ActionLogItem[])

Nested: TeamMember
- `id`, `name`, `email`, `iconBase64`, `permissions` (Permission[])

Example:
```json
{
  "id": "team-1",
  "name": "Dev Guild",
  "iconBase64": null,
  "owner": { "id": "u1", "name": "Alice", "email": "alice@example.com", "permissions": ["ALL"] },
  "members": [],
  "applications": { "app-1": ["MANAGE_SERVERS", "ACCESS_SERVERS"] },
  "invitedMembers": ["bob@example.com"],
  "inviteCode": "ABCD1234",
  "actionLog": []
}
```
