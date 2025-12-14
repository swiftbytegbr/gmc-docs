# Parse INI

Parse a raw INI file into a structured map.

- Method: POST
- Path (REST): `/setting/profile/parse-ini`
- Body: `{ "content": "..." }` (FileBody)
- Returns: `Map<String, Map<String, Object>>`

=== "Java"

    ```java
    FileBody body = new FileBody().setFile("[ServerSettings]\nMaxPlayers=64");
    java.util.LinkedHashMap<String, java.util.LinkedHashMap<String, Object>> parsed =
        gmc.settingProfileClient().parseIni(body).execute();
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
