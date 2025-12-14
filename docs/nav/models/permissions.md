# Model: Permission

Defines access capabilities within a team. Common values:
- `ACCESS_TEAM`, `MANAGE_TEAM`
- `ACCESS_NODES`, `MANAGE_NODES`
- `ACCESS_SERVERS`, `MANAGE_SERVERS`
- `ACCESS_PROFILES`, `MANAGE_PROFILES`
- `ACCESS_AUTOMATIONS`, `MANAGE_AUTOMATIONS`
- `ALL` (full access)

Legacy compatibility values may be present (`VIEW_PROFILES`, `VIEW_TEAM`), but policy decisions are based on the canonical set above.
