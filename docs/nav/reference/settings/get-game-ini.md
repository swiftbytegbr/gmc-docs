# Get game.ini

Fetch the raw game.ini text for a profile.

- Method: GET
- Path (REST): `/setting/profile/{profileId}/game.ini`
- Returns: text/plain

=== "Java"
```java
String gameIni = client.settingProfileClient().getGameIni("prof-1").execute();
```

=== "JavaScript"
```ts
const gameIni = await client.settingProfileClient.getGameIni('prof-1');
```

=== "Python"
```python
game_ini = client.setting_profile_client.get_game_ini('prof-1')
```

=== "REST"
```bash
curl -s https://api.gamemanager.cloud/setting/profile/prof-1/game.ini
```
