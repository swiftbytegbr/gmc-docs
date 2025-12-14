# Model: Node

Represents a registered machine capable of running game servers.

Fields:
- `id` (string): Unique node identifier.
- `teamId` (string): Owning team.
- `inviteToken` (int): Token used during node bootstrap.
- `daemonVersion` (string): Node agent version string.
- `lastAlive` (ISO datetime): Last heartbeat time seen by the backend.
- `lastLogin` (ISO datetime): Last successful authentication.
- `logoutReason` (string|null): Reason for last disconnect, if any.
- `status` (enum): `ONLINE`, `OFFLINE`, `CREATION`.
- `settings` (object): Node settings structure.
- `systemData` (object): System metrics like CPU, RAM, storage.

Example:
```json
{
  "id": "node-123",
  "teamId": "team-1",
  "inviteToken": 123456,
  "daemonVersion": "1.5.2",
  "lastAlive": "2025-01-01T12:34:56Z",
  "lastLogin": "2025-01-01T12:30:00Z",
  "logoutReason": null,
  "status": "ONLINE",
  "settings": { /* implementation specific */ },
  "systemData": { /* cpu/ram/disk fields */ }
}
```
