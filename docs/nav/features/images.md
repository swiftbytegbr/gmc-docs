# Images & Files

Some resources in GMC are binary assets (icons, images, downloadable content). These endpoints return or accept raw bytes (for uploads) instead of JSON. SDKs provide convenience methods to download bytes; for uploads, use multipart/form‑data in REST or the helper methods in SDKs.

## Java
```java
byte[] bytes = client.imageClient().getImage("img-123").execute();
Files.write(Path.of("output.png"), bytes);
```

## JavaScript
```ts
const bytes = await client.imageClient.getImage('img-123');
// bytes is a Buffer in Node.js
```

## Python
```python
img = client.image_client.get_image('img-123')
with open('output.png', 'wb') as f:
    f.write(img)
```

## REST
- `GET /images/{imageId}` (binary)
