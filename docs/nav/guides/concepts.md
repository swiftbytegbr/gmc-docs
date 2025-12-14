# Concepts & Architecture

GMC consists of a cloud backend, a node agent running on your machines, and clients (web app, API/SDK consumers). The backend is the source of truth and coordinates actions; the node agent executes operations like starting servers or creating backups. SDKs talk to the backend over HTTPS with team‑scoped credentials.

Key ideas:
- Team scoping: All data and operations are bound to a team.
- Long‑running tasks: Mutating operations enqueue work on nodes. Check status through runs/logs.
- Idempotency: Most POSTs are safe to retry; conflicting state returns a 409 with a descriptive error key.
- Consistency: Read operations reflect backend state; node telemetry (statistics) may be slightly delayed.
