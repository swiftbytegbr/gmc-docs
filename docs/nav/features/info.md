# Info & Version

Check API and environment information.

## Java
```java
var version = client.infoClient().getVersion().execute();
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

