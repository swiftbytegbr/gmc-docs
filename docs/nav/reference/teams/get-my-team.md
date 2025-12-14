# Get My Team

Return the team associated with your application credentials. This also allows SDKs to cache `teamId`.

- Method: GET
- Path (REST): `/team/my`
- Returns: Team
- Backend behavior: Returns the first/primary team for the application user. 404 if not linked to any team.

## Response
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

=== "Java"
```java
var team = client.teamClient().getTeam(); // synchronous call
String teamId = team.getId();
```

=== "JavaScript"
```ts
const team = await client.teamClient.getTeam();
const teamId = team.id;
```

=== "Python"
```python
team = client.team_client.get_team()
team_id = team.id
```

=== "REST"
```bash
curl -s -H "Accept: application/json" \
  -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
  https://api.gamemanager.cloud/team/my
```
