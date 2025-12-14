# Python Client

The Python SDK is synchronous (uses `requests`). Initialize once to cache `team_id` on the client.

## Setup
```python
from gmc_sdk.client import GmcClient  # WIP package name

client = GmcClient(app_id='<APP_ID>', app_secret='<APP_SECRET>', base_url='https://api.gamemanager.cloud')
# or: GmcClient(app_token='<APP_TOKEN>')
client.initialize()  # populates client.team_id
```

## Usage

### Nodes
```python
nodes = client.node_client.get_nodes()
node = client.node_client.get_node('node-123')
client.node_client.update_node('node-123')
```

### Servers
```python
servers = client.server_client.get_game_servers()
srv = client.server_client.get_game_server('srv-123')

client.server_client.start_server('srv-123')
client.server_client.restart_server('srv-123')
client.server_client.stop_server('srv-123')

created = client.server_client.create_server('node-123', 'My Server', 'CS2', 'de_dust2', '/servers/cs2')

client.server_client.backup_server('srv-123', 'pre-update')
client.server_client.delete_backup('srv-123', 'backup-1')
client.server_client.reset_settings('srv-123')
client.server_client.rcon_command('srv-123', 'status')
```

### Teams
```python
team = client.team_client.get_team()
client.team_client.invite_member('dev@example.com')
client.team_client.kick_member('user-123')
client.team_client.set_permission('user-123', ['ADMIN'])
notifications = client.team_client.get_notifications(only_unread=True)
unread = client.team_client.get_unread_notification_count()
```

### Automations
```python
automations = client.automation_client.list_automations()
created = client.automation_client.create_automation({ 'teamId': client.team_id, 'name': 'Nightly Restart' })
run = client.automation_client.trigger_manual(created.id, { 'targetIds': [] })
```

### Info & Images & Settings
```python
version = client.info_client.get_version()
img_bytes = client.image_client.get_image('img-123')
profile = client.setting_profile_client.get_profile('prof-1')
ini = client.setting_profile_client.get_game_ini('prof-1')
```

## Errors
Errors raise `GmcApiException` (HTTP error with status and key) or `GmcClientException` (connection/unknown). Use try/except:

```python
from gmc_sdk.exceptions import GmcApiException, GmcClientException

try:
    client.server_client.start_server('srv-404')
except (GmcApiException, GmcClientException) as e:
    print(e)
```

## Concurrency
The Python SDK is synchronous. For parallelism, use threads or processes if needed.

