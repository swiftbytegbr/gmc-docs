# JavaScript Client

The JavaScript/TypeScript SDK is Promise-based and supports both ESM and CJS. Initialize once to cache `teamId`.

## Setup
```ts
import { GmcClient } from '@swiftbyte/gmc-sdk'; // WIP package name

const client = new GmcClient({
  appId: process.env.GMC_APP_ID!,
  appSecret: process.env.GMC_APP_SECRET!,
  baseUrl: 'https://api.gamemanager.cloud'
});

await client.initialize(); // fetches team and populates client.teamId
```

## Usage

### Nodes
```ts
const nodes = await client.nodeClient.getNodes();
const node = await client.nodeClient.getNode('node-123');
await client.nodeClient.updateNode('node-123');
```

### Servers
```ts
const servers = await client.serverClient.getGameServers();
const srv = await client.serverClient.getGameServer('srv-123');

await client.serverClient.startServer('srv-123');
await client.serverClient.restartServer('srv-123');
await client.serverClient.stopServer('srv-123');

const created = await client.serverClient.createServer('node-123', 'My Server', 'CS2', 'de_dust2', '/servers/cs2');

await client.serverClient.backupServer('srv-123', 'pre-update');
await client.serverClient.deleteBackup('srv-123', 'backup-1');
await client.serverClient.resetSettings('srv-123');
await client.serverClient.rconCommand('srv-123', 'status');
```

### Teams
```ts
const team = await client.teamClient.getTeam();
await client.teamClient.inviteMember('dev@example.com');
await client.teamClient.kickMember('user-123');
await client.teamClient.setPermission('user-123', ['ADMIN']);
const notifications = await client.teamClient.getNotifications(true);
const unread = await client.teamClient.getUnreadNotificationCount();
```

### Automations
```ts
const automations = await client.automationClient.listAutomations();
const created = await client.automationClient.createAutomation({ teamId: client.teamId!, name: 'Nightly Restart' });
const run = await client.automationClient.triggerManual(created.id, { targetIds: [] });
```

### Info & Images & Settings
```ts
const version = await client.infoClient.getVersion();
const bytes = await client.imageClient.getImage('img-123');
const profile = await client.settingProfileClient.getProfile('prof-1');
const ini = await client.settingProfileClient.getGameIni('prof-1');
```

## Errors
Errors throw `GmcApiException` (HTTP error with status and key) or `GmcClientException` (network/unknown). Use try/catch:

```ts
try {
  await client.serverClient.startServer('srv-404');
} catch (e) {
  console.error(e);
}
```

## Concurrency
Use `Promise.all` for parallel calls:
```ts
const [nodes, servers] = await Promise.all([
  client.nodeClient.getNodes(),
  client.serverClient.getGameServers(),
]);
```

