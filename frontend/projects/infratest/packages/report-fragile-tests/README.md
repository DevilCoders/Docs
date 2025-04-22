# @yandex-int/report-fragile-tests

API, которое позволяет попроектно сообщать конкретным `vteam` о наличии у них хрупких тестов. В работе опирается на результаты графиков `fragile-tests`. Подробнее о хрупких тестах и графиках можно прочитать в [документации](https://wiki.yandex-team.ru/search-interfaces/infra/charts/fragile-tests/).

## Используемые переменные окружения
* `CLICKHOUSE_USER` – имя пользователя, имеющего доступ к кластеру [infra](https://yc.yandex-team.ru/folders/foogt64s2mvid58h88fg/managed-clickhouse/cluster/mdb93hb3hj9nthd6mme3)
* `CLICKHOUSE_PASSWORD` – пароль пользователя для доступа к кластеру
* `REPORT_TESTS_LIMIT` – кол-во сообщаемых хрупких тестов на один `vteam` (по умолчанию `10`)
* `STARTREK_ENTRYPOINT` – адрес API трекера (по умолчанию `https://st-api.yandex-team.ru`)
* `STARTREK_MAX_RETRIES` – максимальное кол-во ретраев при запросе к API `Startrek` (по умолчанию `5`)
* `STARTREK_TIMEOUT_MS` – таймаут запроса к API (по умолчанию `60000` ms)
* `STARTREK_TOKEN` – токен для доступа к API, как получить написано в [документации](https://docs.yandex-team.ru/cloud/tracker/concepts/access)
* `STARTREK_ISSUE_TAG` – тег, который будет добавляться всем созданным тикетам (по умолчанию `hermione-fragile-tests`)
* `NODE_EXTRA_CA_CERTS` – путь на файловой системе к сертификату `YandexInternalRootCA.crt`, скачать можно по [ссылке](https://crls.yandex.net/YandexInternalRootCA.crt)

## Установка

```shell
npm i @yandex-int/report-fragile-tests --registry=https://npm.yandex-team.ru
```

## Использование

Для работы в функцию нужно передать конфигурацию и временной промежуток для которого анализируются тесты на хрупкость.

### Формат конфига
```js
{
    web4: { // имя проекта, как он назван на графике
        queue: 'SERP', // очередь в которой будут создаваться тикеты
        tools: ['hermione', 'hermione-e2e'], // инструменты, тесты которых будут анализироваться (hermione и/или hermione-e2e)
        arcPath: 'frontend/projects/web4' // путь к проекту в Арке
    }
}
```

## Пример

```ts
import moment from "moment";
import { reportFragileTests } from "@yandex-int/report-fragile-tests";

reportFragileTests(
    {
        web4: {
        queue: "SERP",
        tools: ["hermione"],
        arcPath: "frontend/projects/web4"
        }
    },
    moment(),
    moment().subtract(1, "M")
).then(() => console.log("Информация о хрупких тестах hermione из web4 за последний месяц передана командам"));
```
