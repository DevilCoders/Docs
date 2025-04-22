# Релизы в infra.yandex-team.ru

Сервис https://infra.yandex-team.ru - это календарь релизов и недоступности сервисов.

При релизах необходимо отправлять туда отбивки о произошедшем релизе. Сделать это можно командой в archon:

```bash
npm run infra -- -c ${pathToConfig} -e ${environmentName} --appVersion ${version}
```

В таком виде эта команда отпишет о релизе указанной версии в указанном окружении.

Конфиг infra.js хранится в папке .config. В нем же хранится список доступных окружений.

Пример конфига:

```js
module.exports = {
    // Поля для запроса в st с возможностью шаблонизации значения версии.
    ticket: {
        Queue: 'SEAREL',
        Summary: 'report-templates/serp/chat@v{{ version }}',
        Tags: 'chat-templates',
    },
    // ID сервиса и окружений в infra.y-t
    serviceId: 123,
    environmentIds: {
        production: 124
    },
    // Шаблоны для отправки в infra.y-t, разбитые по окружениям.
    // Доступные поля тут: https://infra-api.yandex-team.ru/#/Events/post_events
    templates: {
        production: {
            title: 'Релиз v{{ version }}',
            description: '{{ description }}',
        }
    },
};
```

В данном конфиге - environmentName == 'production'.

В качестве шаблона можно использовать только version и description. Поля в шаблонах могут быть любые, которые поддерживает infra.yandex-team.ru: https://infra-api.yandex-team.ru/#/Events/post_events

По версии находится тикет релиза, проверяется, что он протестирован или уже закрыт.

По умолчанию, дата подставляется текущая. Если вы запоздали с отбивкой, то дату можно передать аргументом ```--date``` в формате, понимаемым ```new Date()```. Пример:

```bash
npm run infra -- -с config/infra-web.js -e production --appVersion 0.1.0 --date "2019-07-29T16:45:00+03:00"
```

Полный список параметров, доступных в команде:

| Параметр            | Обязательность   | Значение по умолчанию | Описание |
| ------------------- | ---------------- | --------------------- | -------- |
| -c, --config <path> | Да  |            | Путь до конфига от корня проекта |
| --appVersion <ver>  | Да  |            | Версия релиза |
| -d, --date <date>   | Нет | new Date() | Дата и время релиза |
| -e, --env <env>     | Нет | production | Окружение для деплоя |
|     --no-email      | Нет | Отправлять | Не отправлять рассылку о релизе |
|     --debug         | Нет | false      | DEBUG режим |
|     --dry-run       | Нет | false      | Только попробовать, посмотреть что будет :) |
| -h, --help          | Нет |            | Показать эти подсказки в консоле |
