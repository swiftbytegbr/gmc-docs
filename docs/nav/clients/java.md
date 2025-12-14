# Java Client

Java is the default example language. The Java SDK is thread-safe and exposes typed clients. Every method returns a `GmcAction<T>` which supports synchronous (`execute()`) and asynchronous (`queue(...)`) execution.

## Setup
```java
GmcClient gmc = GmcClient.builder()
    .baseUrl("https://api.gamemanager.cloud")
    .applicationId("<APP_ID>")
    .applicationSecret("<APP_SECRET>")
    // or: .applicationToken("<APP_TOKEN>")
    .build();

String teamId = gmc.getTeamId(); // discovered automatically
```

## Async vs Sync
- Sync: `T value = action.execute();`
- Async: `action.queue(onSuccess, onError);`

```java
// Sync
java.util.List<GameServer> servers = gmc.serverClient().getGameServers().execute();

// Async
gmc.serverClient().getGameServers().queue(
  list -> System.out.println("Servers: " + list.size()),
  err -> err.printStackTrace()
);
```

## Nodes
```java
java.util.List<Node> nodes = gmc.nodeClient().getNodes().execute();
Node node = gmc.nodeClient().getNode("node-123").execute();
gmc.nodeClient().updateNode("node-123").execute();
gmc.nodeClient().changeSettings("node-123", new NodeSettings()).execute();
java.util.List<NodeTask> tasks = gmc.nodeClient().getNodeTasks("node-123").execute();
```

## Servers
```java
// List and get
java.util.List<GameServer> servers = gmc.serverClient().getGameServers().execute();
GameServer srv = gmc.serverClient().getGameServer("srv-123").execute();

// Lifecycle
gmc.serverClient().startServer("srv-123").execute();
gmc.serverClient().restartServer("srv-123").execute();
gmc.serverClient().stopServer("srv-123").execute();
gmc.serverClient().updateServer("srv-123").execute();

// Create
GameServer created = gmc.serverClient()
    .createServer("node-123", "My Server", GameType.CS2, "de_dust2", "/servers/cs2")
    .execute();

// Backups and settings
gmc.serverClient().backupServer("srv-123", "pre-update").execute();
gmc.serverClient().deleteBackup("srv-123", "backup-1").execute();
gmc.serverClient().resetSettings("srv-123").execute();

// Misc
int maxPlayers = gmc.serverClient().getMaxPlayers("srv-123").execute();
gmc.serverClient().rconCommand("srv-123", "status").execute();
gmc.serverClient().changeDirectory("srv-123", "/servers/cs2").execute();
gmc.serverClient().changeDisplayName("srv-123", "Public Server #1").execute();
```

## Teams
```java
Team team = gmc.teamClient().getTeam();
gmc.teamClient().inviteMember("dev@example.com").execute();
gmc.teamClient().kickMember("user-123").execute();
gmc.teamClient().changeMemberPermission("user-123", java.util.List.of(Permission.MANAGE_SERVERS)).execute();
java.util.List<Notification> notifications = gmc.teamClient().getNotifications(true).execute();
long unread = gmc.teamClient().getUnreadNotificationCount().execute();
```

## Automations
```java
java.util.List<Automation> autList = gmc.automationClient().listAutomations().execute();

AutomationCreateRequest createReq = new AutomationCreateRequest();
createReq.setTeamId(gmc.getTeamId());
createReq.setName("Nightly Restart");
Automation createdAutomation = gmc.automationClient().createAutomation(createReq).execute();

AutomationRun run = gmc.automationClient()
  .triggerManual(createdAutomation.getId(), new ManualTriggerRequest())
  .execute();
```

## Info & Images & Settings
```java
// Version info
GmcVersion version = gmc.infoClient().getVersion().execute();

// Image bytes
byte[] bytes = gmc.imageClient().getImage("img-123").execute();

// Setting profiles
SettingProfile profile = gmc.settingProfileClient().getProfile("prof-1").execute();
String gameIni = gmc.settingProfileClient().getGameIni("prof-1").execute();
```

## Errors
All API errors throw `GmcException` (or subclass). You can read status, key, and message from the exception.

```java
try {
  gmc.serverClient().startServer("srv-404").execute();
} catch (GmcException e) {
  System.err.println(e.getMessage());
}
```
