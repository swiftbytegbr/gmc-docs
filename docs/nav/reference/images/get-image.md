# Get Image

Fetch raw bytes of an image asset by ID.

- Method: GET
- Path (REST): `/images/{imageId}`
- Returns: image bytes (binary)
- Response headers:
  - `Content-Type`: detected from file signature (png, jpeg, gif, webp; otherwise `application/octet-stream`)
  - `Cache-Control`: `public, max-age=2592000, immutable`
  - `Last-Modified`: creation timestamp
  - `Content-Disposition`: `inline; filename="{imageId}.{ext}"`

=== "Java"

    ```java
    byte[] bytes = gmc.imageClient().getImage("img-123").execute();
    ```

=== "JavaScript"

    ```ts
    const bytes = await client.imageClient.getImage('img-123'); // Buffer
    ```

=== "Python"

    ```python
    img = client.image_client.get_image('img-123')
    ```

=== "REST"

    ```bash
    curl -s -o out.png https://api.gamemanager.cloud/images/img-123
    ```
