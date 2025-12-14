# Delete Automation Run

Delete a run record by ID.

- Method: POST
- Path (REST): `/automation-run/{runId}/delete`
- Returns: 200 OK

=== "Java"

    ```java
    gmc.automationRunClient().deleteRun("run-1").execute();
    ```

=== "JavaScript"

    ```ts
    await client.automationRunClient.deleteRun('run-1');
    ```

=== "Python"

    ```python
    client.automation_run_client.delete_run('run-1')
    ```

=== "REST"

    ```bash
    curl -X POST -H "Application-Token: $GMC_APP_TOKEN" \
      https://api.gamemanager.cloud/automation-run/run-1/delete
    ```
