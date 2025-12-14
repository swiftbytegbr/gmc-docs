# Parse INI

Parse a raw INI file into a structured map.

- Method: POST
- Path (REST): `/setting/profile/parse-ini`
- Body: `{ "content": "..." }` (FileBody)
- Returns: `Map<String, Map<String, Object>>`

=== "Java"
```java
var ini = new LinkedHashMap<String, LinkedHashMap<String, Object>>();
var parsed = client.settingProfileClient().parseIni(new FileBody("[ServerSettings]\nMaxPlayers=64")).execute();
```

=== "JavaScript"
```ts
const parsed = await client.settingProfileClient.parseIni({ content: "[ServerSettings]\nMaxPlayers=64" });
```

=== "Python"
```python
parsed = client.setting_profile_client.parse_ini({ 'content': '[ServerSettings]\nMaxPlayers=64' })
```

=== "REST"
```bash
curl -X POST -H "Content-Type: application/json" \
  -d '{"content":"[ServerSettings]\\nMaxPlayers=64"}' \
  https://api.gamemanager.cloud/setting/profile/parse-ini
```
