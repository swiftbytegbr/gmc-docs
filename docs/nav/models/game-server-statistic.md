# Model: GameServerStatistic

Aggregated statistics for a server, keyed by timestamp.

Fields:
- `serverId` (string)
- `dataMap` (object): map from ISO timestamp → data
  - `players` (int)
  - `ramBytes` (long)
  - `cpuPercentage` (int)
  - `networkBytes` (long)

Example:
```json
{
  "serverId": "srv-123",
  "dataMap": {
    "2025-01-01T12:00:00Z": { "players": 10, "ramBytes": 2147483648, "cpuPercentage": 27, "networkBytes": 123456789 }
  }
}
```
