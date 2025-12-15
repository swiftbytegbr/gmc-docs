# REST API

This page describes the common patterns used by GMC REST endpoints so you can call them directly.

- Base URL: `https://api.gamemanager.cloud`
- Authentication: send either `Application-Token` or both `Application-Id` and `Application-Secret`
- Team scope: many endpoints require `teamId` in the path; discover via `GET /team/my`

## Conventions
- JSON input and output
- Standard HTTP methods and status codes
- Error responses contain an error `key` and human-readable `message`
- Pagination for list endpoints via `page` and `size` query params, returning a `Page<T>`

## Discover teamId
```bash
curl -s \
  -H "Accept: application/json" \
  -H "Application-Id: <APP_ID>" \
  -H "Application-Secret: <APP_SECRET>" \
  https://api.gamemanager.cloud/team/my
```

## Examples by Area

### Nodes
- List by team: `GET /node/by-team/{teamId}`
- Get by id: `GET /node/{nodeId}`

```bash
curl -s \
  -H "Accept: application/json" \
  -H "Application-Token: $GMC_APP_TOKEN" \
  https://api.gamemanager.cloud/node/by-team/$TEAM_ID
```

### Servers
- List by team: `GET /server/by-team/{teamId}`
- Get by id: `GET /server/{serverId}`
- Start/Stop/Restart: `POST /server/{serverId}/start|stop|restart`
- Create: `POST /server/create` (JSON body includes `nodeId`, `name`, `gameType`, `map`)

```bash
# Start a server
curl -X POST \
  -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
  https://api.gamemanager.cloud/server/$SERVER_ID/start
```

### Teams
- Get my team: `GET /team/my`
- Invite member: `POST /team/{teamId}/invite` (JSON: `userEmail`)
- Kick member: `POST /team/{teamId}/kick` (JSON: `memberId`)
- Upload icon (multipart): `POST /team/{teamId}/icon`

```bash
# Upload icon
curl -X POST \
  -H "Application-Token: $GMC_APP_TOKEN" \
  -F icon=@icon.png \
  https://api.gamemanager.cloud/team/$TEAM_ID/icon
```

### Automations
- List by team: `GET /automation/by-team/{teamId}`
- Create: `POST /automation`
- Edit: `POST /automation/{automationId}`
- Trigger manual: `POST /automation/{automationId}/trigger/manual`
- List runs: `GET /automation-run/by-team/{teamId}`

### Info & Images & Settings
- Version info: `GET /info/version`
- Download image bytes: `GET /images/{imageId}`
- Update setting profiles: endpoints under `/setting-profile/...`

## Errors
Errors include:
```json
{
  "key": "TEAM_NOT_FOUND",
  "message": "No team for the provided credentials"
}
```
- 400 Bad Request: invalid input
- 401 Unauthorized: invalid/missing credentials
- 403 Forbidden: not allowed for the team
- 404 Not Found: resource missing
- 5xx: server errors

## Pagination
List endpoints may support pagination:
- Query: `?page=0&size=25`
- Response shape: `{ "content": [ ... ], "page": { ... } }` (Page<T>)
