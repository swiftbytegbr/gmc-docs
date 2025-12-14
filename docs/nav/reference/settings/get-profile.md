# Get Setting Profile

Fetch a setting profile by ID.

- Method: GET
- Path (REST): `/setting/profile/{profileId}`
- Returns: SettingProfile

=== "Java"

    ```java
    SettingProfile profile = client.settingProfileClient().getProfile("prof-1").execute();
    ```

=== "JavaScript"

    ```ts
    const profile = await client.settingProfileClient.getProfile('prof-1');
    ```

=== "Python"

    ```python
    profile = client.setting_profile_client.get_profile('prof-1')
    ```

=== "REST"

    ```bash
    curl -s -H "Application-Token: $GMC_APP_TOKEN" \
      https://api.gamemanager.cloud/setting/profile/prof-1
    ```
