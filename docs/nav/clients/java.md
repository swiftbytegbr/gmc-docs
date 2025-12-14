# Java Client

Java is the default example language. The Java SDK is thread-safe and exposes typed clients. Every method returns a `GmcAction<T>` which supports synchronous (`execute()`) and asynchronous (`queue(...)`) execution.

## Setup
```java
import de.swiftbyte.gmc.sdk.GmcClient;

GmcClient client = GmcClient.builder()
    .baseUrl("https://api.gamemanager.cloud")
    .applicationId("<APP_ID>")
    .applicationSecret("<APP_SECRET>")
    // or: .applicationToken("<APP_TOKEN>")
    .build();

String teamId = client.getTeamId(); // discovered automatically
```

## Async vs Sync
- Sync: `T value = action.execute();`
- Async: `action.queue(onSuccess, onError);`

```java
// Sync
var servers = client.serverClient().getGameServers().execute();

// Async
client.serverClient().getGameServers().queue(
  list -> System.out.println("Servers: " + list.size()),
  err -> err.printStackTrace()
);
```

## Nodes
```java
var nodes = client.nodeClient().getNodes().execute();
var node = client.nodeClient().getNode("node-123").execute();
client.nodeClient().updateNode("node-123").execute();
client.nodeClient().changeSettings("node-123", new NodeSettings()).execute();
var tasks = client.nodeClient().getNodeTasks("node-123").execute();
```

## Servers
```java
// List and get
var servers = client.serverClient().getGameServers().execute();
var srv = client.serverClient().getGameServer("srv-123").execute();

// Lifecycle
client.serverClient().startServer("srv-123").execute();
client.serverClient().restartServer("srv-123").execute();
client.serverClient().stopServer("srv-123").execute();
client.serverClient().updateServer("srv-123").execute();

// Create
var created = client.serverClient()
    .createServer("node-123", "My Server", GameType.CS2, "de_dust2", "/servers/cs2")
    .execute();

// Backups and settings
client.serverClient().backupServer("srv-123", "pre-update").execute();
client.serverClient().deleteBackup("srv-123", "backup-1").execute();
client.serverClient().resetSettings("srv-123").execute();

// Misc
int maxPlayers = client.serverClient().getMaxPlayers("srv-123").execute();
client.serverClient().rconCommand("srv-123", "status").execute();
client.serverClient().changeDirectory("srv-123", "/servers/cs2").execute();
client.serverClient().changeDisplayName("srv-123", "Public Server #1").execute();
```

## Teams
```java
var team = client.teamClient().getTeam();
client.teamClient().inviteMember(team.getId(), "dev@example.com").execute();
client.teamClient().kickMember(team.getId(), "user-123").execute();
client.teamClient().setPermission(team.getId(), "user-123", List.of("ADMIN")).execute();
client.teamClient().deleteTeam(team.getId()).execute();
var notifications = client.teamClient().getNotifications(team.getId(), true).execute();
int unread = client.teamClient().getUnreadNotificationCount(team.getId()).execute();
```

## Automations
```java
var autList = client.automationClient().listAutomations().execute();

var createReq = new AutomationCreateRequest();
createReq.setTeamId(client.getTeamId());
createReq.setName("Nightly Restart");
var createdAutomation = client.automationClient().createAutomation(createReq).execute();

var run = client.automationClient()
  .triggerManual(createdAutomation.getId(), new ManualTriggerRequest())
  .execute();
```

## Info & Images & Settings
```java
// Version info
var version = client.infoClient().getVersion().execute();

// Image bytes
byte[] bytes = client.imageClient().getImage("img-123").execute();

// Setting profiles
var profile = client.settingProfileClient().getProfile("prof-1").execute();
String gameIni = client.settingProfileClient().getGameIni("prof-1").execute();
```

## Errors
All API errors throw `GmcException` (or subclass). You can read status, key, and message from the exception.

```java
try {
  client.serverClient().startServer("srv-404").execute();
} catch (GmcException e) {
  System.err.println(e.getMessage());
}
```

