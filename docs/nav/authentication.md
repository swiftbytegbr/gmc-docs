# Authentication

GMC uses application-level credentials that are scoped to a team. This means the permissions and data you can access are bounded by the team that owns the credentials. You can authenticate in one of two ways:

- Application Token (single header)
- Application Id + Application Secret (two headers)

Where to get keys: `app.gamemanager.cloud` → Team Settings → Applications. Keys are team-scoped.

## REST Headers

=== "Application Token"

    ```http
    Application-Token: gmc-app-token-xxxxxxxx
    ```

=== "Id + Secret"

    ```http
    Application-Id: <APP_ID>
    Application-Secret: <APP_SECRET>
    ```

Always send `Accept: application/json`. POST/PUT should send `Content-Type: application/json` unless using multipart.

## Base URLs
- Production: `https://api.gamemanager.cloud`
- Development: Varies (set via client `baseUrl`)

## Team Scope and teamId
- REST endpoints often require a `teamId` path segment, e.g. `/team/{teamId}/...`.
- SDK clients discover `teamId` automatically:
  - Java: on client construction
  - JavaScript: call `await client.initialize()`
  - Python: call `client.initialize()`

## Example
=== "curl"

    ```bash
    curl -H "Accept: application/json" \
         -H "Application-Id: $GMC_APP_ID" \
         -H "Application-Secret: $GMC_APP_SECRET" \
         https://api.gamemanager.cloud/team/my
    ```
