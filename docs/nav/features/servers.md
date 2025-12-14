# Servers

Servers are the heart of GMC: a server represents a running game instance on a node. The backend stores metadata (game type, map, paths) and coordinates lifecycle operations (start/stop/restart/update) as well as configuration and data operations (backup/rollback/directory changes). Only backup, rollback, and directory change operations create a task entry; other actions execute directly and do not create server tasks.

You can use these endpoints to provision servers, manage their configuration, run RCON commands, and keep them updated. When actions are not instantaneous (e.g., backups) the backend responds quickly and the node performs work asynchronously.

## What you can do
List and fetch servers, start/stop/restart/update them, send RCON commands, create/restore backups, and change metadata like the server’s directory and display name.

## Java
```java
java.util.List<GameServer> servers = client.serverClient().getGameServers().execute();
GameServer srv = client.serverClient().getGameServer("srv-123").execute();
client.serverClient().startServer("srv-123").execute();
client.serverClient().restartServer("srv-123").execute();
client.serverClient().stopServer("srv-123").execute();
client.serverClient().updateServer("srv-123").execute();
GameServer created = client.serverClient().createServer("node-123", "My Server", GameType.CS2, "de_dust2", "/servers/cs2").execute();
client.serverClient().backupServer("srv-123", "pre-update").execute();
client.serverClient().deleteBackup("srv-123", "backup-1").execute();
client.serverClient().resetSettings("srv-123").execute();
client.serverClient().rconCommand("srv-123", "status").execute();
client.serverClient().changeDirectory("srv-123", "/servers/cs2").execute();
client.serverClient().changeDisplayName("srv-123", "Public #1").execute();
```

## JavaScript
```ts
const servers = await client.serverClient.getGameServers();
await client.serverClient.startServer('srv-123');
const created = await client.serverClient.createServer('node-123', 'My Server', 'CS2', 'de_dust2', '/servers/cs2');
```

## Python
```python
servers = client.server_client.get_game_servers()
client.server_client.start_server('srv-123')
created = client.server_client.create_server('node-123', 'My Server', 'CS2', 'de_dust2', '/servers/cs2')
```

## REST
- List by team: `GET /server/by-team/{teamId}`
- Get by id: `GET /server/{serverId}`
- Start/Stop/Restart: `POST /server/{serverId}/start|stop|restart`
- Update: `POST /server/{serverId}/update`
- RCON: `POST /server/{serverId}/rcon` (JSON: `{\"command\":\"status\"}`)
- Create: `POST /server/create` (JSON includes `nodeId`, `name`, `gameType`, `map`, `serverDirectory`)
- Backups: `POST /server/{serverId}/backup`, `POST /server/{serverId}/delete-backup`
