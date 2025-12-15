# Errors & Troubleshooting

GMC returns structured errors with an error key and message. SDKs map these to exceptions.

## Error shapes
```json
{
  "key": "TEAM_NOT_FOUND",
  "message": "No team for the provided credentials"
}
```

## Java
- Base: `GmcException`
- Notable subclasses: `BadRequestException`, `UnauthorizedException`, `ForbiddenException`, `NotFoundException`, `ServerErrorException`

```java
try {
  gmc.serverClient().startServer("srv-404").execute();
} catch (GmcException e) {
  System.err.println(e.getMessage());
}
```

## JavaScript
- `GmcApiException`: HTTP error with `statusCode`, `errorKey`, `method`, `url`
- `GmcClientException`: network/unknown

```ts
try {
  await gmc.serverClient.startServer('srv-404');
} catch (e) {
  console.error(e);
}
```

## Python
- `GmcApiException`: HTTP error with `status_code`, `error_key`
- `GmcClientException`: connection/unknown

```python
try:
    gmc.server_client.start_server('srv-404')
except Exception as e:
    print(e)
```

## Common issues
- 401 Unauthorized: Check headers and that key belongs to the correct team
- 403 Forbidden: Operation not permitted for your application user or team
- 404 Not Found: Resource id is wrong or not accessible within your team
- Multipart uploads: Ensure proper `Content-Type` and form field name

