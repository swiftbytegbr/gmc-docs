# List Nodes (by team)

Lists all nodes accessible to your team. The SDKs automatically resolve your `teamId`; REST requires it in the path.

- Method: GET
- Path (REST): `/node/by-team/{teamId}`
- Returns: Array of Node objects
- Backend behavior: returns only nodes belonging to the team from your credentials. No side effects. Cache-friendly.

=== "Java"

    ```java
    java.util.List<Node> nodes = client.nodeClient().getNodes().execute();
    ```

=== "JavaScript"

    ```ts
    const nodes = await client.nodeClient.getNodes();
    ```

=== "Python"

    ```python
    nodes = client.node_client.get_nodes()
    ```

=== "REST"

    ```bash
    curl -s \
      -H "Accept: application/json" \
      -H "Application-Id: $GMC_APP_ID" \
      -H "Application-Secret: $GMC_APP_SECRET" \
      https://api.gamemanager.cloud/node/by-team/$TEAM_ID
    ```

## Responses
- 200 OK: List of nodes.
- 403 Forbidden: `missingPermission.ACCESS_NODES` — you lack read access in this team.
- 404 Not Found: `general.not_found` — team not found.
- 400 Bad Request: `validation.failed` — invalid `teamId` format.
