# Async & Concurrency

Some clients support asynchronous calls for most methods. This section explains how.

## Java
All API methods return `GmcAction<T>`.

- Synchronous: `T value = action.execute();` (blocks until result)
- Asynchronous: `action.queue(onSuccess, onError);` (non-blocking)

```java
gmc.serverClient().getGameServers().queue(
  servers -> System.out.println("Servers: " + servers.size()),
  error -> error.printStackTrace()
);
```

Chaining: compose with futures/promises in your app or queue nested calls in success callbacks.

## JavaScript
All methods return Promises. Use `await` or `.then()`.

```ts
const [nodes, servers] = await Promise.all([
  client.nodeClient.getNodes(),
  gmc.serverClient.getGameServers(),
]);
```

## Python
The Python SDK is currently synchronous. For concurrent work, use threads (e.g., `concurrent.futures.ThreadPoolExecutor`) or async wrappers around blocking calls.

## REST
HTTP is naturally synchronous per request. For concurrency, perform requests in parallel (e.g., multiple processes/threads or async clients) as appropriate for your stack.

## TeamId behavior
- SDKs discover and cache `teamId` at initialization, so you generally do not pass `teamId` to client methods.
- REST endpoints typically require `teamId` in the path. Discover it via `GET /team/my` and reuse.

