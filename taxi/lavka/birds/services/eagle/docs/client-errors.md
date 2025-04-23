# Клиентские ошибки

[Проект в error booster](https://error.yandex-team.ru/projects/lavka-eagle)

Подробнее об error booster [тут](https://wiki.yandex-team.ru/error-booster/)

## Использование

``` ts
import {logError} from 'client/lib/error-logger';

const error = new Error('Some Error');

logError(error, {
    prefix: 'mutationFn', // Контекст ошибки для более быстрого поиска. Например, имя функции, где произошла ошибка
    additional, // Объект без вложенностей,
    message: 'some message', // Сообщение, которое приклеится к error.message
});
```

В `environment == development` ошибки не отправляются в error booster

## Алерты

Оповещения об алертах приходят только в `environment == production`

### Создание

1. Заходим в `Error booster > Settings > Алерты` и используем [эту инструкцию](https://wiki.yandex-team.ru/error-booster/alerts/)

2. Идём на Juggler в раздел [Notification rules](https://juggler.yandex-team.ru/notification_rules/?query=recipient%3Dlavka-eagle-alerts), жмём `Создать` и вводим следующие данные

Селекторы (через &):
`namespace=error-booster-alerts`, `tag=error-booster-project-lavka-eagle`,`tag=error-booster-type-NewErrors`(Count|CountNewErrors|NewErrors|TrendErrors тип алерта из error booster), `service=alert-123`(номер алерта из error booster)

```
namespace=error-booster-alerts
& tag=error-booster-project-lavka-eagle
& tag=error-booster-type-NewErrors
& service=alert-123
```

Неймспейс: `eagle frontend` (создать новый можно [тут](https://juggler.yandex-team.ru/namespaces/?query=namespace=eagle-frontend))

Получатели: `lavka-eagle-alerts` (чат в телеграме)

Способ отправки: `telegram`


### Если пришёл алерт

В сообщении алерта находится ссылка на ошибки в error booster. По сообщениям и дополнительной информации определяем источник ошибок и заводим новую задачу [на доске проекта](https://st.yandex-team.ru/agile/board/15052)

Каждую ошибку отдельно можно найти во вкладке Items в error booster