Title: AEL Examples Cookbook

Discord Webhook – Run Summary
Content
```
Run {automation.name} – step {step.indexHuman}/{run.workflowSize}

Targets ({targets.all.size}): {join(targets.all.names, ', ')}
Succeeded ({targets.succeeded.size}): {join(targets.succeeded.names, ', ')}
Failed ({targets.failed.size}): {join(targets.failed.names, ', ')}
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
{targets.all.size > 3 ? 'Rolling stop' : 'Quick stop'} on {targets.all.size} servers
```

Condition – Status‑Aware Text
```
Step {step.indexHuman} evaluated. Succeeded: {targets.succeeded.size}, Skipped/Failed: {targets.failed.size}
```

Only Active Targets
```
Active: {join(targets.active.names, ', ')}
```

Filtered Lists
```
EU: {join(targets.all.names.?[#this.startsWith('EU-')], ', ')}
```

Uppercase Projection
```
{join(targets.succeeded.names.![upper(#this)], ', ')}
```

Defensive Defaults
```
Backup name: {backupName ?: 'unnamed'}
```

Per‑Target RCON Access
```
First response: {outputs.rcon('cap').byId(targets.all.ids[0]).response ?: 'no response'}

Bullet List of Targets
```
- Total: {targets.all.size}
- Names:\n{join(targets.all.names.![('- ' + #this)], '\n')}
```

Conditional Sections
```
{targets.failed.size > 0 ? 'Some targets failed:' : 'All targets succeeded.'}\n
{targets.failed.size > 0 ? join(targets.failed.names.![('• ' + #this)], '\n') : ''}
```

Fallback Defaults
```
Backup: {backupName ?: (automation.name + '-' + date)}
```

Filter by Prefix
```
EU targets: {join(targets.all.names.?[#this.startsWith('EU-')], ', ')}
NA targets: {join(targets.all.names.?[#this.startsWith('NA-')], ', ')}
```

RCON Await Pattern
```
Step 1 (RCON): set var = cap
Step 2 (Discord): include {join(outputs.rcon('cap').responses, '\n---\n')} to make AUTO awaiting kick in.
```
```
