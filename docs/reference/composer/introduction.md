# Platformatic Composer

Platformatic Composer is an HTTP server that automatically aggregates multiple
services APIs into a single API.

:::info
Platformatic Composer is currently in [public beta](#public-beta).
:::

## Features

- Command-line interface: [`platformatic composer`](/reference/cli.md#composer)
- Automatic [OpenApi composition](/reference/composer/configuration.md#composer)
- [Reverse proxy](/reference/composer/configuration.md#composer) for composed services
- Add custom functionality in a [Fastify plugin](/reference/composer/plugin.md)
- Write plugins in JavaScript or [TypeScript](/reference/cli.md#compile)

## Public beta

Platformatic Composer is in public beta. You can use it in production, but it's quite
likely that you'll encounter significant bugs.

If you run into a bug or have a suggestion for improvement, please
[raise an issue on GitHub](https://github.com/platformatic/platformatic/issues/new).

## Standalone usage

If you're only interested in the features available in Platformatic Composer, you can replace `platformatic` with `@platformatic/composer` in the `dependencies` of your `package.json`, so that you'll import fewer deps.

## Example configuration file

The following configuration file can be used to start a new Platformatic
Composer project. For more details on the configuration file, see the
[configuration documentation](/reference/composer/configuration.md).

```json
{
  "$schema": "https://platformatic.dev/schemas/v0.26.0/composer",
  "server": {
    "hostname": "127.0.0.1",
    "port": 0,
    "logger": {
      "level": "info"
    }
  },
  "composer": {
    "services": [
      {
        "id": "auth-service",
        "origin": "https://auth-service.com",
        "openapi": {
          "url": "/documentation/json",
          "prefix": "auth"
        }
      },
      {
        "id": "payment-service",
        "origin": "https://payment-service.com",
        "openapi": {
          "url": "/documentation/json"
        }
      }
    ],
    "refreshTimeout": 1000
  },
  "watch": true
}
```
