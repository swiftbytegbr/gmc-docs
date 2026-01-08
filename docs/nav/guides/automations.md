Title: Automations Guide

Overview
- Automations let you orchestrate multi-step workflows across servers: start/stop, backups, setting sync, RCON, waits, notifications, webhooks, and more.
- Each automation defines a target set, a trigger, and an ordered workflow of steps.

Key Concepts
- Targets: explicit IDs, dynamic filters, or trigger-source driven.
- Triggers: manual, scheduled (cron), or state-change.
- Steps: actions (start/stop/restart/update/backup/setting-sync), RCON commands, waits (timed/state), and messaging (notify/Discord webhook).
- Timeouts: per-step `timeoutSec` and optional run-level `runTimeoutSec` end long-running workflows.

RCON (Smart Await)
- RconCommand step options:
  - `command` (string)
  - `var` (string, optional): capture name for responses
  - `awaitMode` (AUTO|ALWAYS|NEVER; default AUTO)
  - `timeoutMs` (number, optional)
- AUTO awaits only if a later step references `outputs.rcon('<var>')` in templates. Otherwise it fires-and-forgets.
- ALWAYS forces awaiting; NEVER disables it.

Expression Language
- See “Expression Language (AEL)” for full details.
- Use in Notify/Discord templates to reference run/step/targets and captured outputs.
 - Also see: “AEL Cheatsheet” for a quick reference and “AEL Examples” for copy‑paste snippets.

Best Practices
- Keep steps small; prefer explicit waits over long timeouts.
- Use `var` only when you will consume responses, to avoid unnecessary awaiting.
- Set conservative `timeoutMs` for RCON awaits; use run-level timeouts to cap total execution.
- Validate templates with staging runs to avoid expression errors.

Error Handling
- Step-level failure marks active targets FAILED. Runs continue per normal rules (non-succeeded targets get skipped for subsequent steps).
- Expression errors fail the step with `automation.expression_error` and skip side-effects (no notifications/webhooks sent).

SDKs
- Java: `AutomationClient` and model classes under `de.swiftbyte.gmc.sdk.model.automation`.
- JavaScript: `AutomationResource` and models in `src/models/automation.ts`.
- Python: models in `gmc_sdk.models.automation`.
