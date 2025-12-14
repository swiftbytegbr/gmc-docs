# Copy ARK Profiles

Copy ARK-related setting profiles (useful for migrating between servers or profiles).

- Method: POST
- Path (REST): `/setting/profile/copy`
- Body: `CopyProfileRequest`
- Returns: 204 No Content

=== "Java"

    ```java
    var req = new CopyProfileRequest();
    // req.setSource(...); req.setTargets(...);
    client.settingProfileClient().copyArkProfiles(req).execute();
    ```

=== "JavaScript"

    ```ts
    await client.settingProfileClient.copyArkProfiles({ /* fields */ });
    ```

=== "Python"

    ```python
    client.setting_profile_client.copy_ark_profiles({ /* fields */ })
    ```

=== "REST"

    ```bash
    curl -X POST -H "Content-Type: application/json" \
      -d '{"...":"..."}' \
      https://api.gamemanager.cloud/setting/profile/copy
    ```
