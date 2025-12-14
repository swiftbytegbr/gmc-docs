# Rate Limiting & Retries

The API may apply rate limiting to protect service reliability. Design clients to be resilient:
- Detect HTTP 429 (Too Many Requests) and back off using exponential retry with jitter.
- Prefer bulk/list retrieval with pagination over many small requests.
- Avoid polling tight loops; prefer event-driven triggers or reasonable intervals.

Mutating endpoints are generally idempotent in practice: if an action is already in the desired state (e.g., starting an already running server), the backend responds with a conflict/error key rather than performing duplicate work.
