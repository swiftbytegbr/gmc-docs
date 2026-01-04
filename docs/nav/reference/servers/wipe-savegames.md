Title: Wipe Savegames

Endpoint
- POST `/server/{serverId}/wipe-savegames`

Description
- Deletes all savegame data for the specified server. Requires the server to be OFFLINE. Intended for fresh starts or clean resets.

Permissions
- `MANAGE_SERVERS` on the server’s team.

Request
- Path: `serverId` (string)
- Body: none

Responses
- 200 OK: operation enqueued, event broadcast to team
- 409 Conflict: server is not OFFLINE
- 404 Not Found: server not found

SDK Usage
- JavaScript
  - `await client.serverClient.wipeSavegames(serverId)`
- Java
  - `serverClient.wipeSavegames(serverId).sync()`
- Python
  - `client.server.wipe_savegames(server_id)`

Notes
- This operation is irreversible. Ensure you have backups if needed.
