# Configs

<style>[alt=diagram]{width:1720px}</style>
![diagram](./assets/new-config-diagram.jpg)

## Виды конфигов

| конфиг | обновление в рантайме | где хранится | доступ в коде |
| ------- | ---------------------- | ---------- | ------------- |
| `StartupConfig` | никогда | `локально` | глобальный, `cfg.startup` |
| `DynamicConfig` | каждую минуту | `/dev/configs` | глобальный, `cfg.getDynamic()` + `cfg.addListener()` |
| `RequestConfig` | каждый запрос | `/dev/configs` <- `/experiments3` | контекстный, `req.config` или `useConfig()` |

## Примеры кода

StartupConfig

```ts
import { cfg } from 'lib/config'

const appVersion = cfg.startup.application.version
```

DynamicConfig

```ts
import { cfg } from 'lib/config'

const { loggerLevel } = cfg.getDynamic()

logger.setLevel(loggerLevel)

cfg.addListener(({ loggerLevel }) => {
  logger.setLevel(loggerLevel)
})
```

RequestConfig

```ts
// server
app.use((req, res, next) => {
  if (req.config.ssrEnabled) {
    // ...
  }
})

// ssr+browser
const Component = () => {
  const config = useConfig()

  if (config.ssrEnabled) {
    // ...
  }
}
```

## Локальные конфиги

```ts
interface YandexCfg {
  startup: StartupConfig
  dynamic: DynamicConfig // фолбэк когда сервис недоступен
  request: RequestConfig // фолбэк когда сервис недоступен
}

// полное описание в файле defaults.ts
const config: YandexCfg = {
  startup: { ... },
  dynamic: { ... },
  request: { ... },
}

// частичные переопределения в остальных
const config: DeepPartial<YandexCfg> = {
  startup: {
    logger: {
      level: 'error',
    },
  },
}
```

## Как добавить конфиг в тестовую админку

1. Добавляем yaml схему в группу [lavka-website](../../../../../schemas/schemas/configs/declarations/lavka-website/)
2. Создаем PR, добавляем ему тэг `taxi/deploy:testing`
3. Ждем пока пройдут все `teamcity-taxi` проверки
4. Заходим в [teamcity](https://teamcity.taxi.yandex-team.ru/viewType.html?buildTypeId=YandexTaxiProjects_Tools_Schemas_Customs_CustomTestingArcadia) и открываем `Run` через `...`
5. В параметре `update_only_group_schemas` указываем нашу группу `lavka-website` и нажимаем `Run Build`
6. После раскатки конфиги можно найти в админке: https://tariff-editor.taxi.tst.yandex-team.ru/dev/configs?group=lavka-website

## Как добавить конфиг в продовую админку

1. Мерджим PR в транк
2. Заходим в [teamcity](https://teamcity.taxi.yandex-team.ru/viewType.html?buildTypeId=YandexTaxiProjects_Tools_Schemas_Releases_AutoRelease) и открываем `Run` через `...`
3. В параметре `update_only_group_schemas` указываем нашу группу `lavka-website` и нажимаем `Run Build`
4. После раскатки конфиг можно найти в админке: https://tariff-editor.taxi.yandex-team.ru/dev/configs?group=lavka-website

## Как удалить конфиг

1. Переходим на страницу скриптов: [тестинг](https://tariff-editor.taxi.tst.yandex-team.ru/dev/scripts?created_by=%3Ame), [прод](https://tariff-editor.taxi.yandex-team.ru/dev/scripts?created_by=%3Ame)
2. Нажимаем `Новый скрипт` и заполняем необходимые поля
3. Нажимаем сохранить
4. Просим апрувы (или апрувим сами в случае тестинга)

Пример скрипта в тестинге: https://tariff-editor.taxi.tst.yandex-team.ru/dev/scripts/d4d1986f5ab64cf09164653ed81cf0ce

```
[URL скрипта]
https://bb.yandex-team.ru/projects/TAXI/repos/tools-py3/browse/taxi_config_schemas/db/remove_config.py

[PYTHONPATH]
/usr/lib/yandex/taxi-config-schemas/

[Аргументы]
all-configs-values
--clean-with-schema
--names
LAVKA_WEBSITE_DYNAMIC_CONFIG_1
LAVKA_WEBSITE_DYNAMIC_CONFIG_2
LAVKA_WEBSITE_REQUEST_CONFIG_1
LAVKA_WEBSITE_REQUEST_CONFIG_2

[Описание]
Удаление неисползуемых конфигов
```

## Ссылки

- [Схемы конфигов](https://wiki.yandex-team.ru/taxi/backend/architecture/configs/Manual/#validatoryijsonsxemy)
- [JSON схемы](https://json-schema.org/understanding-json-schema/)

