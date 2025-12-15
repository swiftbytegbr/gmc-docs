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

=== "Java"

    ```java
    Team team = client.teamClient().getTeam(); // synchronous call
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
