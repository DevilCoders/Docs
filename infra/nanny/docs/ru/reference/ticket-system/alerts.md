# Alert Workflow

## Alert {#alert}

Задача Alert в Nanny — донести информацию о событиях, которые могут повлиять на релизный цикл сервиса. Alert можно привязать к очередям/метаочередям, в этом случае информация будет отображена на страницах очереди и всех связанных тикетов.

{% note warning %}

Если не указать набор очередей/метаочередей, alert будет применяться ко всем очередям/метаочередям.

{% endnote %}

![img](https://jing.yandex-team.ru/files/sshipkov/alertpanel.08e8676.png)

## Статусы тикетов {#ticket-status}

* В момент начала действия алерта для очереди все тикеты в состояниях `IN_QUEUE`, `COMMITED` будут переведены в `ON_HOLD`.
* В произвольный момент к тикету может быть привязано произвольное количество алертов.
* Новые тикеты, появившиеся в очереди после начала действия алерта, остаются в состоянии `IN_QUEUE`.
* После снятия всех алертов с очереди / метаочереди, возвращается состояние тикета до выставления фриза. Относится только к тем тикетам, чей статус не менялся все это время (могут быть тикеты, чьи статусы были сменены, значит с ними кто то работает и статус их более трогать не стоит).
* Если на момент создания алерта тикет находился в состоянии `ON_HOLD`, после снятия алерта его состояние не изменится.
* Если алерт удаляется, его действие заканчивается досрочно, тикеты меняют свои статусы (если требуется).
* В тикете будут оставлены комментарии о начале/окончании действия/удалении алерта.

## Выгрузка событий из календаря {#export-activity}

В Nanny есть сервис [Alert_syncer](https://nanny.yandex-team.ru/ui/#/services/catalog/alert_syncer/)

1. Получает события из [ календаря плановых работ](https://calendar.yandex-team.ru/week?embed&private_token=46440d714afcb9394b6e4f5cb555b15ea5d37940&tz_id=Europe/Moscow) на ближайшие 30 дней.
1. События со спецразметкой синхронизируются в alert'ы в Nanny.

Чтобы синхронизировать событие, нужно:
1. пригласить nanny-robot@
1. в "Место встречи" вставить json со значениями привязываемых очередей

    пример:

    ```json
    {"queue": ["Q1", "Q2"], "meta_queue": ["MQ"]}
    ```

    Если оставить "Место встречи" пустым или передать два пустых списка, будет установлено значение по умолчанию:

    ```json
    {"meta_queue": ["SEARCHMON"]}
    ```
