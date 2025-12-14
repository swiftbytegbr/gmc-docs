# Latest Node Version

Get the latest available node version string.

- Method: GET
- Path (REST): `/node/latest-version`
- Returns: string version
- Backend behavior: Indicates the backend-supported node version. Useful to check update availability.

=== "Java"

    ```java
    String version = gmc.nodeClient().getLatestVersion().execute();
    ```

=== "JavaScript"

    ```ts
    const version = await client.nodeClient.getLatestVersion();
    ```

=== "Python"

    ```python
    version = client.node_client.get_latest_version()
    ```

=== "REST"

    ```bash
    curl -s https://api.gamemanager.cloud/node/latest-version
    ```
