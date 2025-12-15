# Model: GameServer

Represents a controllable game server on a node.

Core fields (entity):
- `id` (string)
- `displayName` (string)
- `teamId` (string)
- `nodeId` (string)
- `created` (ISO datetime)
- `gameType` (enum): e.g., `ARK_EVOLVED`, `ARK_ASCENDED`
- `state` (enum): runtime state (e.g., `ONLINE`, `OFFLINE`, `RESTARTING`)
- `settingProfileId` (string)
- `serverDirectory` (string)
- `onlinePlayers` (int)
- `backups` (array): Backup metadata
- `commands` (array): Supported RCON commands

Enriched fields (GET responses):
- `nodeName` (string)
- `serverIp` (string)
- `map` (string)
- `maxPlayers` (int)
- `modCount` (int)
- `serverPort` (int)
- `queryPort` (int)
- `rconPort` (int)

Example:
```json
{
  "id": "srv-123",
  "displayName": "Public #1",
  "nodeId": "node-123",
  "created": "2025-01-01T12:00:00Z",
  "teamId": "team-1",
  "gameType": "ARK_ASCENDED",
  "state": "RUNNING",
  "settingProfileId": "prof-1",
  "serverDirectory": "/servers/ark",
  "onlinePlayers": 12,
  "nodeName": "eu-west-1",
  "serverIp": "203.0.113.12",
  "map": "Fjordur",
  "maxPlayers": 64,
  "modCount": 0,
  "serverPort": 27015,
  "queryPort": 27016,
  "rconPort": 27017
}
```
