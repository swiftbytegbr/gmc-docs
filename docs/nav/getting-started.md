# Getting Started

This guide helps you set up credentials, choose a client, and make your first call.

## Requirements
- An active GMC account and a team
- A team-scoped application credential (see “API Keys” below)
- Network access to the GMC API (default: `https://api.gamemanager.cloud`)
- One of:
  - Java 11+ and Maven/Gradle
  - Node.js 18+ (or Deno/Bun with fetch-compatible APIs)
  - Python 3.9+

## API Keys (Team‑Scoped)
- Where: `app.gamemanager.cloud` → Team Settings → Applications
- Scope: Keys are team-scoped; every action happens within your team context.
- Forms:
  - Application Token (single header)
  - Application Id + Application Secret (two headers)

You can rotate or revoke keys in Team Settings.

## Installation (WIP)
Note: Packages are not yet published to Maven Central, npm, or PyPI.

- Java (WIP): Will be published under `de.swiftbyte.gmc:gmc-java-sdk`.
- JavaScript (WIP): Will be published as `@swiftbyte/gmc-sdk`.
- Python (WIP): Will be published as `gmc-sdk`.

Until then, build from source in the sibling repos:
- `../gmc-java-sdk`
- `../gmc-js-sdk`
- `../gmc-python-sdk`

## First Call

> Tip: Use the language tabs to switch code examples. Your selection persists across pages (enabled via `content.tabs.link`).

=== "Java (default)"

    ```java
    GmcClient gmc = GmcClient.builder()
        .baseUrl("https://api.gamemanager.cloud")
        .applicationId("<APP_ID>")
        .applicationSecret("<APP_SECRET>")
        // or: .applicationToken("<APP_TOKEN>")
        .build();

    // Team ID is discovered automatically
    Team team = gmc.teamClient().getTeam();
    System.out.println("Team: " + team.getName());
    ```

=== "JavaScript"

    ```ts
    import { GmcClient } from '@swiftbyte/gmc-sdk'; // WIP package name
    
    const client = new GmcClient({
      appId: process.env.GMC_APP_ID!,
      appSecret: process.env.GMC_APP_SECRET!,
      baseUrl: 'https://api.gamemanager.cloud'
    });
    
    await client.initialize(); // fetches and caches teamId
    const team = await client.teamClient.getTeam();
    console.log('Team:', team.name);
    ```

=== "Python"

    ```python
    from gmc_sdk.client import GmcClient  # WIP package name
    
    client = GmcClient(app_id="<APP_ID>", app_secret="<APP_SECRET>", base_url="https://api.gamemanager.cloud")
    # or: GmcClient(app_token="<APP_TOKEN>")
    client.initialize()  # populates team_id
    team = client.team_client.get_team()
    print("Team:", team.name)
    ```

=== "REST (curl)"

    ```bash
    # Get my team (discover teamId)
    curl -s \
      -H "Accept: application/json" \
      -H "Application-Id: <APP_ID>" \
      -H "Application-Secret: <APP_SECRET>" \
      https://api.gamemanager.cloud/team/my | jq
    ```

## What’s Next
- Understand authentication details: `nav/authentication.md`
- Explore Java client usage: `nav/clients/java.md`
- Learn REST conventions, errors, and pagination: `nav/rest.md`
