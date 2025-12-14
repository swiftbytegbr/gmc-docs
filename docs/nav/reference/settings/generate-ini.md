# Generate INI

Generate an INI string from a structured map.

- Method: POST
- Path (REST): `/setting/profile/generate-ini`
- Body: `Map<String, Map<String, Object>>`
- Returns: string (INI)

=== "Java"

    ```java
    java.util.LinkedHashMap<String, java.util.LinkedHashMap<String, Object>> map = new java.util.LinkedHashMap<>();
    String ini = client.settingProfileClient().generateIni(map).execute();
    ```

=== "JavaScript"

    ```ts
    const ini = await client.settingProfileClient.generateIni({});
    ```

=== "Python"

    ```python
    ini = client.setting_profile_client.generate_ini({})
    ```

=== "REST"

    ```bash
    curl -X POST -H "Content-Type: application/json" \
      -d '{}' \
      https://api.gamemanager.cloud/setting/profile/generate-ini
    ```
