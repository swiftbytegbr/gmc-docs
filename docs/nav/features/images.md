# Images & Files

Work with image/content endpoints, typically returning raw bytes.

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

