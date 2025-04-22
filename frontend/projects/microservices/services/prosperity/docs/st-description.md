# Дополнение описания тикета в Стартреке

Позволяет дополнять описание связанных с ревью-реквестом тикетов трекера по событию `ArcHeadsUpdated` от Arcanum в соответствии с конфигурацией в репозитории.
Событие `ArcHeadsUpdated` в ревью-реквесте происходит на каждый пуш.

> Обновлять описание пулл-реквеста можно и [по событиям из Sandbox][sandbox-update-description].

Требует наличия у [robot-prosperity@] доступа на чтение/запись тикетов хотя бы в одной из очередей, указанных в заголовке пулл-реквеста.

## Настройка

> ⚠️ Если после настройки ничего не работает:
> ошибки при желании можно найти в [логе][prosperity-yd-log]
> или обратиться за помощью в [infraduty].

1. [Выдать доступ][queue-access] на чтение тикетов в используемых очередях роботу [robot-prosperity@].
1. Подключить проект к обработке в [конфиге arcadia-github][arcadia-gh-cfg], если он ещё не подключен. Для этого нужно создать тикет в [infraduty].
1. Создать конфиг в `.config/st-description.(yml|json)` по описанию ниже.

## Конфигурационный файл

Файл может быть в одном из двух форматов: `json` либо `yml`.

### Схема

Конфигурационный файл должен удовлетворять [JSON-схеме][st-description-json-schema].

### Шаблонизация
Шаблонизация происходит таким же образом, как и в [PR description v2][shablonizaciya], но ключ `github_payload` содержит эмулированные на основе данных Арканума данные GitHub.

Пример использования:

```json
{
    "title": "Ссылки для тестирования",
    "links": [
        {
            "label": "Бета",
            "url": "https://renderer-ydo-pull-{{github_payload.pull_request.number}}.hamster.yandex.ru/uslugi/"
        },
        {
            "label": "Storybook",
            "url": "https://frontend-test.s3.mds.yandex.net/story/@yandex-int/ydo/pull-{{github_payload.pull_request.number}}/index.htm",
        }
    ],
    "queues": ["YDO", "SERP"]
}
```

`queues` — список очередей (whitelist), тикеты в которых будут обновлены

* Получим такой набор ссылок:

![image](./images/st-descr-example.png)

[robot-prosperity@]: https://staff.yandex-team.ru/robot-prosperity
[st-description-json-schema]: ../schema/st-description.json
[sandbox-update-description]: ./st-update-description.md
[shablonizaciya]: ./pr-description-v2.md#shablonizaciya
[customlinks]: ./pr-description-v2.md#customlinks
[queue-access]: https://doc.yandex-team.ru/tracker/external/manager/queue-access.html#queue-access
[arcadia-gh-cfg]: https://genisys.yandex-team.ru/rules/search-interfaces.arcadia-github/default
[prosperity-yd-log]: https://deploy.yandex-team.ru/stage/prosperity/logs
[infraduty]: https://wiki.yandex-team.ru/infraduty/
