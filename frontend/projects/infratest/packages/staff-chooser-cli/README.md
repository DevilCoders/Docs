# staff-chooser-cli

> CLI для [staff-chooser].

## Особенности обёртки

* шаблонизация средствами ejs;
* вывод сообщений в Slack;

## Установка

```shell
npm install @yandex-int/si.ci.staff-chooser-cli --registry=https://npm.yandex-team.ru
```

## Использование

```shell
staff-chooser abc:infraspeed --template "Утренник ведёт <%= name.first.ru %> <%= name.last.ru %> (@<%= login %>)"
```

## Описание 

Выбор случайного сотрудника.

Что делает:
* выбирает сотрудников из нескольких источников: список логинов, сервисы ABC;
* принимает шаблон сообщения и наполняет его данными выбранного сотрудника;
* отправляет сообщение в Slack;

Сервисы ABC указываются с префиксом "abc:".

Структура данных сотрудника для шаблона сообщения: [схема][persons-schema].
На данный момент из данных сотрудника доступно только поле `login`, см. [STAFF-17398](https://st.yandex-team.ru/STAFF-17398).
Чтобы использовать другие поля, нужно дозаказать роботу доступы для них.

## Доступные опции

```shell
  -t, --template               Шаблон сообщения в формате ejs.
  -w, --include-gap-workflows  Включаемые типы отсутствий.               [array]
  -x, --exclude-gap-workflows  Исключаемые типы отсутствий.              [array]
  -r, --include-abc-roles      Включаемые роли сотрудников из ABC сервисов.
                                                                         [array]
  -s, --exclude-abc-roles      Исключаемые роли сотрудников из ABC сервисов.
                                                                         [array]
  -c, --slack-channel          Идентификатор канала в Slack (необходимо указать
                               переменную окружения SLACK_TOKEN).
  -d, --date                   Дата в формате "YYYY-MM-DD", на которую
                               происходит выбор.
  -h, --help                   Show help                               [boolean]
  -v, --version                Show version number                     [boolean]
```

[staff-chooser]: https://a.yandex-team.ru/arcadia/frontend/projects/infratest/packages/staff-chooser
[persons-schema]: https://staff-api.yandex-team.ru/_static/v3/api/schemas/person.json
