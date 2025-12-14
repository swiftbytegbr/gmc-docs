# Get Server Statistics

Fetch live or cached server statistics. Note: Path includes nodeId per current API.

- Method: GET
- Path (REST): `/{nodeId}/{serverId}/statistics`
- Returns: GameServerStatistic
- Backend behavior: Hits the node agent; may be cached briefly. Requires server to be reachable.

=== "Java"

    ```java
    GameServerStatistic stats = gmc.serverClient().getStatistics("node-123", "srv-123").execute();
    ```

=== "JavaScript"

    ```ts
    const stats = await client.serverClient.getStatistics('node-123', 'srv-123');
    ```

=== "Python"

    ```python
    stats = client.server_client.get_statistics('node-123', 'srv-123')
    ```

=== "REST"

    ```bash
    curl -s -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
      https://api.gamemanager.cloud/node-123/srv-123/statistics
    ```
