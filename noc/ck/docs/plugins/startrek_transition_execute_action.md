# startrek_transition_execute - изменить статус startrek-тикета

Startrek вместо прямой смены статуса тикета на произвольный статус позволяет использовать
фиксированный workflow, описываемый переходами (transitions). Каждая очередь имеет свой workflow.
Возможные переходы из текущего состояния в интерфейсе Startrek видны над описанием тикета:

![Переходы в интерфейсе Startrek](_assets/startrek_transitions.png "Переходы в интерфейсе Startrek" =777x317)

При этом каждый переход может предполагать заполнение экранных полей (screen fields). Например, при
закрытии тикета можно указать резолюцию

Данный action как раз позволяет изменять статус тикетов выполнением таких переходов

{% note info %}

Если при выполнении этого action ЦК получает ошибку от Startrek с HTTP-статусом 404 и текстом
_Переход не существует_, то причиной может быть следующее:

- у пользователя, от имени которого ЦК работает со Startrek, отсутствуют права на редактирование
  задач очереди (пример:
  [NOCREQUESTS-36013](https://st.yandex-team.ru/NOCREQUESTS-36013#62ce7812eec278776dc43b9b))
- допущена ошибка при указании идентификаторе перехода
- для задачи в её текущем статусе этот переход недоступен

{% endnote %}

## Параметры

- `issue` - тикет в Startrek
- `transition` - идентификатор перехода; его можно найти в поле `id` по запросу актуальных возможных переходов
  конкретной задачи (см "Как найти идентификаторы переходов" ниже)
- `screen_fields` - заполняемые экранные поля в форме перехода

{% note alert %}

При выполнении переходов следует осторожно относиться к заполнению screen fields. Например, были
случаи, когда автоматика закрывала тикеты без Резолюции, и это создавало много проблем. В NOCRFCS
такой проблемы не будет, потому что в screen fields
[проставлено значение по-умолчанию](https://st-api.yandex-team.ru/v2/screens/97950)

{% endnote %}

## Как найти идентификаторы переходов

Допустим, нам нужно сделать переход для задачи из очереди NOCREQUESTS. Находим (или создаём) реальную задачу в этой
очереди в нужном исходном статусе: [NOCREQUESTS-28869](https://st.yandex-team.ru/NOCREQUESTS-28869). Она сейчас в статусе
"Информация получена" (`infoProvided`). Переходим по ссылке
`https://st-api.yandex-team.ru/v2/issues/NOCREQUESTS-28869/transitions` и видим json следующего содержания:
  ```json
[
  {
    "id": "start_progress",
    "self": "https://st-api.yandex-team.ru/v2/issues/NOCREQUESTS-28869/transitions/start_progress",
    "display": "В работу",
    "to": {
      "self": "https://st-api.yandex-team.ru/v2/statuses/4",
      "id": "4",
      "key": "inProgress",
      "display": "В работе"
    }
  },
  {
    "id": "need_info",
    "self": "https://st-api.yandex-team.ru/v2/issues/NOCREQUESTS-28869/transitions/need_info",
    "display": "Нужна информация",
    "to": {
      "self": "https://st-api.yandex-team.ru/v2/statuses/17",
      "id": "17",
      "key": "needInfo",
      "display": "Требуется информация"
    },
    "screen": {
      "self": "https://st-api.yandex-team.ru/v2/screens/8264",
      "id": "8264",
      "display": "8264"
    }
  },
  {
    "id": "close",
    "self": "https://st-api.yandex-team.ru/v2/issues/NOCREQUESTS-28869/transitions/close",
    "display": "Закрыть",
    "to": {
      "self": "https://st-api.yandex-team.ru/v2/statuses/3",
      "id": "3",
      "key": "closed",
      "display": "Закрыт"
    },
    "screen": {
      "self": "https://st-api.yandex-team.ru/v2/screens/223994",
      "id": "223994",
      "display": "223994"
    }
  }
]
  ```
Находим идентификаторы всех возможных переходов из статуса "Информация получена" (`infoProvided`) в свойстве `id`:

- `start_progress`
- `need_info`
- `close`

## Переходы в NOCRFCS

В NOCRFCS есть следующие переходы:

- `inProgress` - "Начать выполнение", переводит тикет из статуса `pending` в статус
  `inProgress`
- `closed` - "Отмена изменения", переводит тикет из статуса `pending` в статус `closed`
- `close` - "Закрыть", переводит тикет из статуса `inProgress` в статус `closed`

## Примеры

После создания NOCRFCS-тикета и до начала его выполнения есть возможность отменить работы. Вот так
выглядит такая отмена выполнения NOCRFCS-тикета:

```yaml
actions:
  - startrek_transition_execute:
      issue: NOCRFCS-7696
      transition: closed  # аналогично нажатию кнопки "Отмена изменения"
      # В резолюции будет проставлено "Отменено"
```

Начать выполнение согласованного NOCRFCS-тикета:

```yaml
actions:
  - startrek_transition_execute:
      issue: NOCRFCS-7696
      transition: inProgress  # аналогично нажатию кнопки "Начать выполнение"
```

Успешно завершить выполнение NOCRFCS-тикета, который сейчас в статусе "В работе":

```yaml
actions:
  - startrek_transition_execute:
      issue: NOCRFCS-7696
      transition: close  # аналогично нажатию кнопки "Закрыть"
      # В резолюции будет проставлено "Сделано"
```

Завершить выполнение NOCRFCS-тикета, который сейчас в статусе "В работе", с кастомной резолюцией:

```yaml
actions:
  - startrek_transition_execute:
      issue: NOCRFCS-7696
      transition: close  # аналогично нажатию кнопки "Закрыть"
      screen_fields:
        # закрыть с резолюцией "Откат изменения" (если не указать, то по-умолчанию проставится
        # "Сделано")
        resolution: Откат изменения
```
