# Update Profile

Update fields in a setting profile.

- Method: POST
- Path (REST): `/setting/profile`
- Body: `SettingProfileUpdateRequest`
- Returns: 204 No Content

=== "Java"

    ```java
    var update = new SettingProfileUpdateRequest();
    update.setProfileId("prof-1");
    client.settingProfileClient().updateProfile(update).execute();
    ```

=== "JavaScript"

    ```ts
    await client.settingProfileClient.updateProfile({ profileId: 'prof-1' /* fields */ });
    ```

=== "Python"

    ```python
    client.setting_profile_client.update_profile({ 'profileId': 'prof-1' })
    ```

=== "REST"

    ```bash
    curl -X POST -H "Content-Type: application/json" \
      -H "Application-Token: $GMC_APP_TOKEN" \
      -d '{"profileId":"prof-1"}' \
      https://api.gamemanager.cloud/setting/profile
    ```
