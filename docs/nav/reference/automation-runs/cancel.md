# Cancel Automation Run

Cancel a run in progress, if supported by the underlying task.

- Method: POST
- Path (REST): `/automation-run/{runId}/cancel`
- Returns: AutomationRun (updated status)

=== "Java"

    ```java
    AutomationRun canceled = client.automationRunClient().cancelRun("run-1").execute();
    ```

=== "JavaScript"

    ```ts
    const canceled = await client.automationRunClient.cancelRun('run-1');
    ```

=== "Python"

    ```python
    canceled = client.automation_run_client.cancel_run('run-1')
    ```

=== "REST"

    ```bash
    curl -X POST -H "Application-Id: $GMC_APP_ID" -H "Application-Secret: $GMC_APP_SECRET" \
      https://api.gamemanager.cloud/automation-run/run-1/cancel
    ```
