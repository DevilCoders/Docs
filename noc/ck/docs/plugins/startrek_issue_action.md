# startrek_issue - создать startrek-тикет

## Параметры

- `queue` - очередь в startrek, набор очередей ограничен следующими возможными значениями:
  - `NOCREQUESTS`
  - `NOCRFCS`
  - `ITDC`
  - `TRASH`
- `issue_type_key` - тип startrek-тикета, все типы можно увидеть прямо в
  [API Startrek](https://st-api.yandex-team.ru/v2/issuetypes), самые популярные примеры:
  - `task` - задача
  - `bug` - ошибка
- `template` - шаблон создания тикетов; параметризуется полями, указанными в `context`; сейчас
  поддерживаются шаблоны:
  - `common` - общий шаблон без кастомизаций
  - `nocrfcs` - шаблон, специфичный для очереди NOCRFCS
- `context` - параметры шаблона; набор параметров зависит от шаблона

## Шаблон common

Самый примитивный шаблон, который позволяет указать название и описание тикета. Параметры:

- `summary` - заголовок тикета
- `description` - описание тикета

## Шаблон nocrfcs

Шаблон рендерит тикеты способом, аналогичным
[форме заведения NOCRFCS](https://forms.yandex-team.ru/surveys/21525/). Описание параметров:

- `name` - название изменения
- `change_type` - тип изменения:
  - `Normal` - плановое изменение
  - `Emergency` - аварийное изменение
- `responsible` - исполнитель
- `infra` - название подсистемы, как в [Infra](infra.yandex-team.ru/):
  - `NOC DEV - Grad`
  - `NOC DEV - HBF`
  - `NOC DEV - Linkeye`
  - `NOC DEV - Puncher`
  - `NOC DEV - Racktables`
  - `NOC DC - Core`
  - `NOC DC - ToR`
  - `NOC DC - CrossDC`
  - `NOC DC - Decap`
  - `NOC DC - DNS64`
  - `NOC DC - Drills`
  - `NOC DC - Firewall`
  - `NOC DC - IPMI`
  - `NOC DC - NAT64`
  - `NOC DC - TUN64`
  - `NOC FFC - Network`
  - `NOC FFC - WiFi`
  - `NOC Office - Conference`
  - `NOC Office - Network`
  - `NOC Office - WiFi`
  - `NOC Office - DynFW`
  - `NOC Office - IPTel`
  - `NOC Office - Regional`
  - `NOC Office - VPN`
  - `NOC TT - CDN`
  - `NOC TT - DNS`
  - `NOC TT - HEX`
  - `NOC TT - L3 Balancers`
  - `NOC TT - L3 Manager`
  - `NOC TT - RTN Manager`
  - `NOC Border - BGP`
- `datacenters` - область применения изменения, список датацентров, возможные датацентры:
  - `ДЦ VLA`
  - `ДЦ MAN`
  - `ДЦ SAS`
  - `ДЦ IVA`
  - `ДЦ MYT`
  - `Другое`
- `previous_experience` - предыдущий опыт/успех изменения:
  - `Был опыт и он был успешным`
  - `Был успешный опыт, но в прошлый раз в процессе возникали проблемы`
  - `Другое`
- `is_automated` - автоматизировано изменение (`true`) или нет (`false`); очевидно, что тут (почти)
  всегда должно быть `true`
- `change_testing` - тестирование изменения; в случае `is_automated = false` должно быть указано; в
  случае `is_automated = true` не должно быть указано
  - `Юнит-тесты и интеграционные тесты`
  - `Только юнит-тесты`
  - `Тестировалось вручную`
  - `Не тестировалось`
- `service_impact` - влияние на сервис:
  - `Да`
  - `Нет`
  - `Неизвестно`
- `services` - список сервисов, на которое будет (потенциальное) влияние влияние; в случае
  `service_impact`, равном `Да` или `Неизвестно`, должно быть указано; в случае `service_impact`,
  равном `Нет`, не должно быть указано; возможные значения - ABC-сервисы
- `influence_rollback` - длительность влияния и откат; в случае `service_impact`, равном `Да` или
  `Неизвестно`, должно быть указано; в случае `service_impact`, равном `Нет`, не должно быть
  указано; возможные значения:
  - `Без прерывания, быстрый откат`
  - `Без прерывания, длительный откат`
  - `Прерывание на короткое время, быстрый откат`
  - `Другое`
- `start` - дата-время начала работ, обазятельно
- `end` - дата-время окончания работ, обазятельно
- `description` - описание изменения, обазятельно
- `preparation` - план подготовки к изменению, опционально
- `execution` - план выполнения изменения, обязательно
- `rollback` - план отката изменения, обазятельно

## Примеры

Создание тикета по шаблону nocrfcs в очереди NOCRFCS, получится аналогичное тикету
[NOCRFCS-8458](https://st.yandex-team.ru/NOCRFCS-8458):

```yaml
name: create-issue-test
actions:
  - startrek_issue:
      # Указываем очередь в Startrek
      queue: NOCRFCS
      # Указываем тип тикета: задача
      issue_type_key: task
      # Выбираем один из шаблонов: сейчас поддерживаются nocrfcs и common
      template: nocrfcs
      # Указываем контекст для рендеринга тикета по выбранному
      context:
        name: Снятие трафика с линка man1-x2 100ge5/0/3 - man-36d8 e32/1
        change_type: Normal
        responsible: ekulemzin
        infra: NOC DC - Core
        datacenters:
          - ДЦ MAN
        previous_experience: Был опыт и он был успешным
        is_automated: false
        change_testing: Не тестировалось
        service_impact: Нет
        start: "2021-07-25T01:19:00+03:00"
        end: "2021-07-25T01:29:00+03:00"
        description: >-
            %%(diff)Diff for man1-x2:
            interface 100GE5/0/3
            + description man-36d8 e32/1 damaged
            -   eth-trunk 368
            -   portswitch
            %%
        # preparation:
        execution: >-
            Patch for man1-x2:
            interface 100GE5/0/3
             description man-36d8 e32/1 damaged
                undo eth-trunk
                undo portswitch
        rollback: Не предусмотрено
```

Можно также создать тикет по шаблону nocrfcs в очереди TRASH для тестирования:

```yaml
name: create-issue-test
actions:
  - startrek_issue:
      # Указываем очередь в Startrek
      queue: TRASH
      # Указываем тип тикета: задача
      issue_type_key: task
      # Выбираем один из шаблонов: сейчас поддерживаются nocrfcs и common
      template: nocrfcs
      # Указываем контекст для рендеринга тикета по выбранному
      context:
        name: Снятие трафика с линка man1-x2 100ge5/0/3 - man-36d8 e32/1
        change_type: Normal
        responsible: ekulemzin
        infra: NOC DC - Core
        datacenters:
          - ДЦ MAN
        previous_experience: Был опыт и он был успешным
        is_automated: false
        change_testing: Не тестировалось
        service_impact: Нет
        start: "2021-07-25T01:19:00+03:00"
        end: "2021-07-25T01:29:00+03:00"
        description: >-
            %%(diff)Diff for man1-x2:
            interface 100GE5/0/3
            + description man-36d8 e32/1 damaged
            -   eth-trunk 368
            -   portswitch
            %%
        # preparation:
        execution: >-
            Patch for man1-x2:
            interface 100GE5/0/3
             description man-36d8 e32/1 damaged
                undo eth-trunk
                undo portswitch
        rollback: Не предусмотрено
```

Создание тикета по шаблону common в очереди TRASH:

```yaml
name: create-issue-test
actions:
  - startrek_issue:
      queue: TRASH
      issue_type_key: task
      template: common
      context:
        summary: Заголовок тикета
        description: Описание тикета
```
