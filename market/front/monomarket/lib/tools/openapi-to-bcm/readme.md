[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=market/monomarket&vcs=github&repoFilter=lib/tools/openapi-to-bcm)](https://oko.yandex-team.ru/github/market/monomarket?repoFilter=lib/tools/openapi-to-bcm) [![oko health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-market/openapi-to-bcm)](https://oko.yandex-team.ru/pkg/@yandex-market/openapi-to-bcm)

# openapi-to-bcm

Генератор типизированного bcm клиента по OpenAPI/Swagger схеме.

## Использование

Установить в проекте как дев зависимость

```
npm install -D @yandex-market/openapi-to-bcm
```

Для удобства использования его можно добавить в npm скрипты в `package.json`

```json
{
    "scripts": {
        "openapi-to-bcm": "openapi-to-bcm --config=./configs/foo.js --lang=flow"
    }
}
```

После чего генерация кода для бекенда из конфига делается с помощью команды

```
npm run openapi-to-bcm -- --name=someBackend
```

## Опции

<!-- GENERATED_START(id:main;hash:70f3e1993cf92b7d05970d52ae3b8eff) This is generated content, do not modify by hand, to regenerate run "yammy build-only me docs" -->
- `--help` Show help.
- `--version` Show version.
- `--quiet` Do not write to stdout. Default is "false"
- `--lang` What syntax to output. Supported: "flow" | "typescript". Default is "typescript"
- `--dest` Path to destination.
- `--config` Path to openapi-to-bcm.config.js
- `--regenerate-script` Script to run to regenerate files.
- `--prettier-config-path` Path to prettier config, if omitted will search for it automatically.
- `--list-presets` List all presets with respected links for openapi schemas and swagger ui. Default is "false"
- `--use-cache` Get backend openapi/swagger schemas from cache if present. Default is "false"
<!-- GENERATED_END(id:main) -->

## Пример конфига


```js
// openapi-to-bcm.js
module.exports = {
    regenerateScript: 'npm run genereate-bcm -- {{presetName}}',
    destination: 'shared/bcm',
    presets: {
        someBackend: {
            swaggerConfig: {
                host: 'https://some-backend.network.net',
                file: 'v2/api-docs',
                ui: '',
            },
            // bcm backend config
            backendConfig: {
                retry: 0,
                timeout: 30000,
                parseBody: 'json',
                encodeBody: 'json',
                agent: {
                    name: 'someBackend',
                    maxSockets: 1000,
                },
            },
        },
        anotherBackend: {
            swaggerConfig: {
                host: 'https://another-backend.network.net',
                file: 'openapi/public-api.yaml',
                ui: 'swagger-ui',
            },
            backendConfig: {
                retry: 0,
                timeout: 30000,
                parseBody: 'json',
                encodeBody: 'json',
                agent: {
                    name: 'anotherBackend',
                    maxSockets: 1000,
                },
                basePackage: '@yandex-market/another-base-fetcher',
            },
        },
    },
};
```
