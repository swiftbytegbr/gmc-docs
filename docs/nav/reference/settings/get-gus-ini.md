# Get GameUserSettings.ini

Fetch the raw GameUserSettings.ini text for a profile.

- Method: GET
- Path (REST): `/setting/profile/{profileId}/gameUserSettings.ini`
- Returns: text/plain

=== "Java"

    ```java
    String gus = client.settingProfileClient().getGameUserSettingsIni("prof-1").execute();
    ```

=== "JavaScript"

    ```ts
    const gus = await client.settingProfileClient.getGameUserSettingsIni('prof-1');
    ```

=== "Python"

    ```python
    gus = client.setting_profile_client.get_game_user_settings_ini('prof-1')
    ```

=== "REST"

    ```bash
    curl -s https://api.gamemanager.cloud/setting/profile/prof-1/gameUserSettings.ini
    ```
