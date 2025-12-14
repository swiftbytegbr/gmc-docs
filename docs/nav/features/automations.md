# Automations

Automations orchestrate sequences of operations on your infrastructure. Think of them as reusable workflows (e.g., nightly restarts, pre‑match scaling, scheduled backups). Automations are team‑scoped; you can create, edit and delete them, and then trigger runs manually or via external scheduling. Each run is tracked with rich status and timestamps.

Automations are great for repeatability and safety. Instead of scripting against raw endpoints, you capture intent once and invoke it whenever needed.

## What you can do
List automations, create/edit/delete them, trigger manual runs, and explore the history and status of runs across your team.

## Java
```java
java.util.List<Automation> list = gmc.automationClient().listAutomations().execute();
AutomationCreateRequest create = new AutomationCreateRequest();
create.setTeamId(gmc.getTeamId());
create.setName("Nightly Restart");
Automation created = gmc.automationClient().createAutomation(create).execute();
AutomationRun run = gmc.automationClient().triggerManual(created.getId(), new ManualTriggerRequest()).execute();
```

## JavaScript
```ts
const list = await client.automationClient.listAutomations();
const created = await client.automationClient.createAutomation({ teamId: client.teamId!, name: 'Nightly Restart' });
const run = await client.automationClient.triggerManual(created.id, { targetIds: [] });
```

## Python
```python
automations = client.automation_client.list_automations()
created = client.automation_client.create_automation({'teamId': client.team_id, 'name': 'Nightly Restart'})
run = client.automation_client.trigger_manual(created.id, {'targetIds': []})
```

## REST
- List: `GET /automation/by-team/{teamId}`
- Create: `POST /automation/create`
- Edit: `POST /automation/{automationId}/edit`
- Delete: `POST /automation/{automationId}/delete`
- Trigger manual: `POST /automation/{automationId}/trigger-manual`
- Runs: `GET /automation-run/by-team/{teamId}`
