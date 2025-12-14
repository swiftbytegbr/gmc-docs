# Get Version

Return backend version information.

- Method: GET
- Path (REST): `/info/version`
- Returns: GmcVersion

=== "Java"

    ```java
    GmcVersion version = client.infoClient().getVersion().execute();
    ```

=== "JavaScript"

    ```ts
    const version = await client.infoClient.getVersion();
    ```

=== "Python"

    ```python
    version = client.info_client.get_version()
    ```

=== "REST"

    ```bash
    curl -s https://api.gamemanager.cloud/info/version
    ```
