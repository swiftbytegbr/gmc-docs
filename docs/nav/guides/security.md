# Security & Compliance

Credentials are application-level and scoped to a team. Rotate them regularly and restrict access according to principle of least privilege using permissions. The backend enforces authorization on every request and logs actions for auditability.

Recommendations:
- Store secrets securely (environment variables or a secret manager).
- Scope app users with granular permissions instead of ALL where possible.
- Monitor the action log (Teams → Action Log) and notifications for security‑relevant events.
- Use HTTPS only; verify base URLs and certificates.
