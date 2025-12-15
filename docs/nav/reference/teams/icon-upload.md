# Upload Team Icon

Upload or replace the team's icon using multipart/form-data.

- Method: POST
- Path (REST): `/team/{teamId}/icon`
- Body: multipart field `icon=@icon.png`
- Returns: 200 OK
- Backend behavior: Replaces the current icon; image is stored and served from the image endpoint (`/images/{imageId}`).

=== "Java"

    ```java
    byte[] bytes = Files.readAllBytes(Path.of("icon.png"));
    client.teamClient().changeTeamIcon(bytes, "icon.png").execute();
    ```

=== "JavaScript"

    ```ts
    // Using FormData in Node with form-data package
    import FormData from 'form-data';
    import fs from 'fs';
    const form = new FormData();
    form.append('icon', fs.createReadStream('icon.png'));
    await client.teamClient.uploadIcon(form);
    ```

=== "Python"

    ```python
    with open('icon.png', 'rb') as f:
        client.team_client.upload_icon(f)
    ```

=== "REST"

    ```bash
    curl -X POST -H "Application-Token: $GMC_APP_TOKEN" \
      -F icon=@icon.png \
      https://api.gamemanager.cloud/team/$TEAM_ID/icon
    ```
