Title: AEL Examples Cookbook

Discord Webhook – Run Summary
Content
```
Run {automation.name} – step {step.indexHuman}/{run.workflowSize}

Targets ({targets.count}): {join(targets.names, ', ')}
Succeeded ({targets.succeededIds.size()}): {join(targets.succeededNames, ', ')}
Failed ({targets.failedIds.size()}): {join(targets.failedNames, ', ')}
```

Discord Webhook – RCON Output Digest
Prereq: RCON step with `var = cap`
```
RCON responses for {automation.name}:
{join(outputs.rcon('cap').responses, '\n---\n')}
```

Notify – Human‑Friendly Timestamps
Title
```
Automation {automation.name}
```
Message
```
Started at {formatDate(epoch, 'yyyy-MM-dd HH:mm:ss', 'UTC')} (UTC)
```

STOP – Conditional Message
```
{targets.count > 3 ? 'Rolling stop' : 'Quick stop'} on {targets.count} servers
```

Condition – Status‑Aware Text
```
Step {step.indexHuman} evaluated. Succeeded: {targets.succeededIds.size()}, Skipped/Failed: {targets.failedIds.size()}
```

Only Active Targets
```
Active: {join(targets.activeNames, ', ')}
```

Filtered Lists
```
EU: {join(targets.names.?[#this.startsWith('EU-')], ', ')}
```

Uppercase Projection
```
{join(targets.succeededNames.![upper(#this)], ', ')}
```

Defensive Defaults
```
Backup name: {backupName ?: 'unnamed'}
```

Per‑Target RCON Access
```
First response: {outputs.rcon('cap').byId(targets.ids[0]).response ?: 'no response'}

Bullet List of Targets
```
- Total: {targets.count}
- Names:\n{join(targets.names.![('- ' + #this)], '\n')}
```

Conditional Sections
```
{targets.failedIds.size() > 0 ? 'Some targets failed:' : 'All targets succeeded.'}\n
{targets.failedIds.size() > 0 ? join(targets.failedNames.![concat('• ', #this)], '\n') : ''}
```

Fallback Defaults
```
Backup: {backupName ?: (automation.name + '-' + date)}
```

Filter by Prefix
```
EU targets: {join(targets.names.?[#this.startsWith('EU-')], ', ')}
NA targets: {join(targets.names.?[#this.startsWith('NA-')], ', ')}
```

RCON Await Pattern
```
Step 1 (RCON): set var = cap
Step 2 (Discord): include {join(outputs.rcon('cap').responses, '\n---\n')} to make AUTO awaiting kick in.
```
```
