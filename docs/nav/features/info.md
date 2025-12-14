# Info & Version

The Info endpoints expose meta information about the backend environment and its version. They are handy for health checks, compatibility checks (e.g., node↔backend versions), and diagnosing connectivity.

## Java
```java
GmcVersion version = client.infoClient().getVersion().execute();
System.out.println("API Version: " + version.getVersion());
```

## JavaScript
```ts
const version = await client.infoClient.getVersion();
console.log('API Version:', version.version);
```

## Python
```python
version = client.info_client.get_version()
print('API Version:', version.version)
```

## REST
- `GET /info/version`
