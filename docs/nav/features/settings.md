# Settings

Setting profiles capture configuration for your servers in a structured way. Besides reading and updating profiles, the backend can also parse classic INI files into structured maps and generate INI text from structured data. This is useful when migrating existing setups or templating configs.

## Java
```java
SettingProfile profile = client.settingProfileClient().getProfile("prof-1").execute();
String gameIni = client.settingProfileClient().getGameIni("prof-1").execute();
String gusIni = client.settingProfileClient().getGameUserSettingsIni("prof-1").execute();

SettingProfileUpdateRequest update = new SettingProfileUpdateRequest();
update.setProfileId("prof-1");
client.settingProfileClient().updateProfile(update).execute();
```

## JavaScript
```ts
const profile = await client.settingProfileClient.getProfile('prof-1');
const gameIni = await client.settingProfileClient.getGameIni('prof-1');
```

## Python
```python
profile = client.setting_profile_client.get_profile('prof-1')
ini = client.setting_profile_client.get_game_ini('prof-1')
```

## REST
- `GET /setting/profile/{profileId}`
- `GET /setting/profile/{profileId}/game.ini`
- `GET /setting/profile/{profileId}/gameUserSettings.ini`
- `POST /setting/profile` (update)
