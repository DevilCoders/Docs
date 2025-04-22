# renderer-betas-cli

_[Общая информация про беты renderer.](https://doc.yandex-team.ru/si-infra/renderer-betas/general.html)_

_renderer-беты основаны на yappy, поэтому полезно будет предварительно ознакомиться с [терминологией yappy](https://wiki.yandex-team.ru/JandeksPoisk/Sepe/yappy/terms/) и, дополнительно, [документацией stoker](https://wiki.yandex-team.ru/jandekspoisk/sepe/stoker/), записями о бетах в котором управляет yappy._

Данная утилита используется для деплоя и других операций с бетами renderer. Позволяет через отдельный [конфиг](#формат-конфигурации) (который может храниться в коде проекта), а также через [опции утилиты](#команды-и-опции-renderer-betas-cli) задать параметры для поднимаемых бет. Все что делают отдельные команды этой утилиты - вызывают те или иные методы [yappy api](https://wiki.yandex-team.ru/JandeksPoisk/Sepe/yappy/api/) в определенной последовательности, позволяющей, например, для команды [create](#create) получить поднятую бету.

Стандартными местами вызова данной утилиты и ее команд являются sandbox или trendbox-таски, которые обычно запускаются при внесении изменений в пулл-реквестах, либо при влитии в master/dev ветку проекта. Примерами таких тасок могут служить [SANDBOX_CI_YAPPY_DEPLOY](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/sandbox_ci/sandbox_ci_yappy_deploy/__init__.py?rev=r7857718#L80), [SANDBOX_CI_WEB4_YAPPY_CLEANUP](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/sandbox_ci/sandbox_ci_web4_yappy_cleanup/__init__.py?rev=r7018156), либо [общая trendbox-таска `Deploy`](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/.trendbox.yml?rev=r8166035#L150) в монорепе frontend.

Альтернативно может использоваться еще один пакет [`frontend.ci.deploy`](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/frontend.ci.deploy?rev=r8066788), который, в частности, оборачивает и утилиту `renderer-betas-cli`. Подробнее о нем в контексте renderer-бет можно прочесть [тут](https://doc.yandex-team.ru/si-infra/renderer-betas/start.html#frontend-ci-deploy).

## Установка

```
npm i @yandex-int/renderer-betas-cli --registry https://npm.yandex-team.ru
```

## Формат конфигурации

Конфигурация `renderer-betas-cli` представляет из себя json-файл, в котором ожидаются следующие поля:

- **id** - обязательное, уникальный id [компонента](https://wiki.yandex-team.ru/JandeksPoisk/Sepe/yappy/terms/#komponent), определяет префикс урла беты. Урл - запись в [stoker](https://wiki.yandex-team.ru/jandekspoisk/sepe/stoker/), которую для каждой беты создает и которой управляет Yappy. Следует указывать начинающийся с `renderer-`.
- **quota** - обязательное, в какой [квоте](https://wiki.yandex-team.ru/JandeksPoisk/Sepe/yappy/terms/#kvota) следует поднимать бету. Подробнее о квотах [в основной документации](https://doc.yandex-team.ru/si-infra/renderer-betas/quotas.html).
- **component** - обязательное, объект со следующими полями:
    - **sourceNames** - обязательное, массив имен источников, которые поднимаемая бета должна подменить.
    - **timeout** - опциональное, таймаут ответа подменяемых источников.
    - **additionalParams** - опциональное, определяет, какие параметры будут добавлены stoker'ом при очередном запросе по урлу беты. Массив строк вида "имя_параметра=значение".
- **auth** - обязательное, определяет, кто может управлять (останавливать, перезапускать, удалять) создаваемой бетой. Если вы не планируете поднимать беты руками, сюда следует вписать релевантных роботов из ci. Объект с полями `logins` и `groups`, одно из которых является обязательным:
    - **logins** - список staff-логинов.
    - **groups** - список идентификаторов abc-сервисов.
- **ttl** - опциональное, время жизни беты, по умолчанию - 7 дней. `ttl` переустанавливается при каждом следующем обновлении беты.
- **bolverOverrides** - опциональное, позволяет переопределить рассмотренные выше опции поля `component` для отдельных бет по указанному суффиксу. Поле `key` определяет какое поле из `component` следует переопределить. Формат можно посмотреть на примере [конфигурации для web4](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/.config/renderer-betas/config.json?rev=9d5d98146ee89aaec4037c938dce51628d2a4732#L19-48).
- **replicate** - опциональное, реплицировать ли создаваемые беты, по умолчанию `true`. Ожидается что для указанной в `quota` квоте существует ее реплика. Подробнее о репликации [в основной документации](https://doc.yandex-team.ru/si-infra/renderer-betas/quotas.html#replikatsiia-bet).

Пример конфигурации:

```json
{
    "id": "renderer-doc-demo",
    "quota": "report-renderer-templates",
    "auth": {
        "groups": [1492]
    },
    "component": {
        "timeout": 5000,
        "sourceNames": ["TEMPLATES", "DOC_DEMO_TEMPLATES", "RENDERER", "RENDERER_DEMO"]
    },
    "ttl": 96
}
```

Для такой конфигурации и `suffix` (опция команды [create](#create)), установленом в `test`, стокерная запись беты будет выглядеть так - `https://renderer-doc-demo-test.hamster.yandex.ru`.

Больше примеров конфигурации можно посмотреть в коде существующих сервисов, например, [ydo](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/ydo/.config/renderer-betas/config.json?rev=r7308165).

## Команды и опции

```
npx @yandex-int/renderer-betas-cli --help
```

### create

Деплой беты.

Обязательные опции:

- **config** - путь до [файла с конфигом](#формат-конфигурации) относительно cwd, либо абсолютный.
- **suffix** - суффикс для имени беты, добавляется к полю `id` из конфига. Для пулл-реквестов типичным используемым значением является `pull-<номер пулл-реквеста>`.
- **resource** - Идентификатор sandbox-ресурса с архивом report-renderer-совместимых шаблонов. Допускается несколько упоминаний, количество зависит от конфигурации yappy-квоты, обычно один.

Необязательные опции:
- **keepForever** - устанавливает `ttl` в бесконечность, переопределяя поле ttl из конфига.
- **overwriteQuota** - позволяет переопределить указанную в конфиге yappy-квоту.
- **allSlots** - флажок, предписывающий в итоговом выводе команды вернуть массив всех слотов, (например, [реплик](https://doc.yandex-team.ru/si-infra/renderer-betas/quotas.html#replikatsiia-bet)), а не строку с первым слотом, в которых размещена бета. По умолчанию не установлен.
- **header** - какие заголовки прописать в стокерной записи беты.
- **collectMetrics** - предпринимать ли попытку сбора solomon-метрик работы утилиты. По умолчанию включено, но также требует наличия переменной окружения `SOLOMON_OAUTH_TOKEN`, отсутствие которой равносильно выключению сбора метрик.
- **metricsOverwrites** - json, позволяет переопределить передаваемые в solomon метрики. По умолчанию -
```js
{
    project: "fei",
    service: "renderer_betas",
    cluster: "sandbox",
    // SANDBOX_TASK_ID - кастомная переменная окружения, определенная в sandbox_ci и trendbox-тасках
    labels: process.env.SANDBOX_TASK_ID ? { task: process.env.SANDBOX_TASK_ID } : {},
}
```

Пример вызова:

```sh
npx @yandex-int/renderer-betas-cli create --config "./.config.json" --suffix "pull-123" --all-slots
```

Дополнительные примеры вызова команды деплоя можно посмотреть в коде существующих сервисов, например, [jobs](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/jobs/tools/deploy-dynamic.js?rev=r8078492#L34).

### delete

Остановка и удаление беты.

Обязательными опциями являются `config` и `suffix`, необязательные - `overwriteQuota`, `collectMetrics` и `metricsOverwrites`. Смысл всех опций совпадает с одноименными опциями команды [`create`](#create).

Примеры вызова команды остановки можно посмотреть в коде существующих сервисов, например, [ydo](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/ydo/tools/deploy-remove.sh?rev=r8173946#L4).

### get-beta-info

Получение слотов, в которых размещена бета.

Обязательными опциями являются `config` и `suffix`, необязательные - `overwriteQuota` и `allSlots`. Смысл всех опций совпадает с одноименными опциями команды [`create`](#create).

Выводит в stdout JSON с полями:

- **betaName** - имя беты.
- **slot** - один слот, либо, если указана опция `allSlots`, массив со списком слотов (fqdn + порт), по которому поднята.

Пример вывода:

```json
{"betaName":"renderer-doc-demo-test","slot":["renderer-betas-4-2.sas.yp-c.yandex.net:4210","renderer-betas-replica-2-1.man.yp-c.yandex.net:4020"]}
```
