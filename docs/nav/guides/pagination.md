# Pagination & Filtering

List endpoints support pagination via `page` (0-based) and `size`. The response is a `Page<T>` structure with total counts and flags (`first`, `last`). Some list endpoints also accept filters via query params.

Recommendations:
- Choose reasonable `size` values (e.g., 25–100) depending on your UI/flow.
- Preserve `page`/`size` in your client state; don't assume single-page results.
- Combine filters to minimize server load and data transfer.
