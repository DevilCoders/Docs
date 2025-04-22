# `@vertis/prometheus`

Package to setup prometheus http-server.

## Usage

```js
const { createServer } = require('@vertis/prometheus');

const server = createServer({
    // Use promClient.register or promClient.AggregatorRegistry
    cluster: boolean, // Default: false.
    // Hostname to bind
    hostname: string, // Default: '::'.
    // Port to listen.
    listen: number,
});
```
