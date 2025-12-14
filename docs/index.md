# GMC Documentation

Welcome to the official API and SDK documentation for Game Manager Cloud (GMC).

Game Manager Cloud itself is a full web application for managing self‑hosted game servers. If you just want to run, update and monitor your servers using a browser, head over to the product site at https://gamemanager.cloud for a tour of the platform. This documentation, in contrast, is focused on the programmatic side of GMC: the REST API and the language SDKs that let you automate and integrate everything GMC can do.

If you are building tools, control panels, bots, or CI/CD pipelines that should provision or operate servers, this is the right place. The SDKs mirror the backend’s capabilities and translate HTTP into straightforward method calls with typed models, robust error handling and (where applicable) asynchronous execution.

## What this documentation covers
You will find step‑by‑step explanations for every feature area (Nodes, Servers, Automations, Teams, Images, Settings, Info). For each individual endpoint we explain:

- What the endpoint does and when you should use it
- How the backend behaves (side‑effects, idempotency, long‑running tasks, expected status codes)
- Any team‑scoping requirements and permission constraints
- Examples in Java (default), JavaScript/TypeScript, Python, and raw REST

Where it adds clarity, we include guidance on sequencing operations (for example: creating a server, then backing it up, then rolling it back) and how the system reacts to errors or conflicts.

## About Game Manager Cloud (product)
Game Manager Cloud is built to operate self‑hosted, dedicated game servers at scale. It manages nodes (machines), game server processes, configuration, backups and automations. The web application is the canonical user interface, and the API/SDKs provide the same capabilities for developers who want to extend or automate the platform.

Learn more about the product at https://gamemanager.cloud.

## About the API and SDKs
- The API is HTTP+JSON with predictable resource paths and error shapes.
- SDKs provide typed clients, input models and unified error handling.
- Credentials are application‑level and team‑scoped. SDKs will discover and cache your `teamId` for you.
- Java and JavaScript SDKs support asynchronous usage; the Python SDK is synchronous.

## Choosing between REST and an SDK
If you want the most direct control, have an existing HTTP client stack, or are integrating from a language without an SDK, use the REST documentation and examples. If you want faster iterations, typed models and built‑in error mapping, use an SDK. You can mix both approaches if needed.

## Quick links
See these pages to get productive quickly:

- Getting Started: `nav/getting-started.md` — requirements, keys, first request
- Authentication: `nav/authentication.md` — headers, base URLs, team scoping
- Java Client (default): `nav/clients/java.md` — idiomatic usage and async
- REST API: `nav/rest.md` — conventions, errors, pagination

