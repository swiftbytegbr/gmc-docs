# Model: Permission

Defines access capabilities within a team.

Available permissions:
- `ACCESS_TEAM`, `MANAGE_TEAM`
- `ACCESS_NODES`, `MANAGE_NODES`
- `ACCESS_SERVERS`, `MANAGE_SERVERS`
- `ACCESS_PROFILES`, `MANAGE_PROFILES`
- `ACCESS_AUTOMATIONS`, `MANAGE_AUTOMATIONS`
- `ALL` (full access)

Legacy compatibility values may be present:
- `VIEW_PROFILES`, `VIEW_TEAM`

Note: There is no `ADMIN` permission. Use the appropriate `MANAGE_*` or `ALL` scope depending on the operation you intend to allow.
