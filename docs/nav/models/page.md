# Model: Page<T>

Standard pagination container.

Fields:
- `content` (T[]): items for the current page
- `page` (int): current page index (0-based)
- `size` (int): requested page size
- `totalElements` (long)
- `totalPages` (int)
- `first`, `last` (boolean)
- `numberOfElements` (int)
- `empty` (boolean)

Example:
```json
{
  "content": [ /* items */ ],
  "page": 0,
  "size": 25,
  "totalElements": 100,
  "totalPages": 4,
  "first": true,
  "last": false,
  "numberOfElements": 25,
  "empty": false
}
```
