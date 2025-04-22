# Deploy в Report-renderer (Yappy)

Для деплоя используется библиотека [@yandex-int/renderer-betas-cli](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/renderer-betas-cli).
Код скрипта находится [здесь](../src/deploy-scripts/report-renderer/report-renderer-deploy-script.ts)<br >

## Формат конфига
Тайпинги для конфига находятся [здесь](../src/deploy-scripts/report-renderer/types.ts)

```(json)
{
    "type": "report-renderer",
    "beta": {
        "resourceType": string; // 'WEB_<ИМЯ СЕРВИСА>_MICRO_PACKAGE'
        "tarball": string; // `<имя сервиса>-templates.tar.gz`
        "rendererBetasCliConfig": Config; //https://github.yandex-team.ru/search-interfaces/infratest/blob/master/packages/renderer-betas-cli/README.md#конфигурация
        "rendererBetasCliOptions"?: {
          "param1": "value1";
        };
    },
    "release": {
        "resourceType": string; // 'WEB_<ИМЯ СЕРВИСА>_MICRO_PACKAGE'
        "tarball": string; // '<имя сервиса>-templates.tar.gz'
    }
}
```

### Примеры

* [Конфиг для беток и релиза](./examples/report-renderer/config.json)
* [Конфиг со сборкой артефакта](./examples/report-renderer/with-artifact.json)
* [Конфиг со сборкой для мастера](./examples/report-renderer/with-master.json)

### Сборка артефакта

Процесс сборки артефакта можно автоматизировать. Для этого нужно добавить секцию `build` в корне конфига ([пример](./examples/report-renderer/with-artifact.json)):
```json
  "build": {
    "dynamic": {
      "tarball": "service-name-templates.tar.gz", // имя артефакта
      "patterns": [ // паттерны, по которым будут добавлены файлы в артефакт
        "pattern1.json",
        "pattern2/**"
      ]
    }
  },
```

Для сборки артефакта используется пакет `tartifacts`, более подробную информацию о синтаксисе паттернов можно найти в документации пакета.

После добавления этих секций в конфиг необходимо добавить флаг `--build` к вызову команды `deploy` в ваших скриптах. Ваша команда будет выглядеть примерно так: `YENV=testing frontend-deploy deploy --config=.config/deploy/config.json --build`.

