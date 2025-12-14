# Model: SettingProfile

Stores configuration for game servers, including INI sections.

Fields:
- `id`, `teamId`
- `gameType` (string)
- `lastModified` (ISO datetime)
- `map` (string)
- `gameSettings` (map<section, map<key, value>>)
- `gameUserSettings` (map<section, map<key, value>>)
- `questionMarkParams` (map)
- `hyphenParams` (map)
- `gmcSettings` (map)

Example:
```json
{
  "id": "prof-1",
  "teamId": "team-1",
  "gameType": "ARK_ASCENDED",
  "lastModified": "2025-01-03T10:00:00Z",
  "map": "Fjordur",
  "gameSettings": { "ServerSettings": { "MaxPlayers": 64 }},
  "gameUserSettings": {},
  "questionMarkParams": {},
  "hyphenParams": {},
  "gmcSettings": {}
}
```
