# Модуля взаимодействия со стартреком tpl-common-startrek

## Основной состав

### StartrekService
_**StartrekService**_ — общий сервис для непосредственного взаимодействия со стартреком.
Он нужен для:
- создания тикетов
- получения существующих
- поиска по тикетам

### StartrekTicket
_**StartrekTicket**_ — класс, предоставляющий интерфейс-обёртку для работы с тикетом. То, что возвращает `StartrekService`.
Он умеет:
- возвращать основную информацию о тикете (ключ, статус, очередь).
- добавлять комментарии к тикету
- создавать связанные тикеты всех видов и получать их
- устанавливать / получать / сбрасывать значения полей тикета **(все поля должны быть предварительно добавлены в перечисление `TicketField`)**
- осуществлять перевод тикета в доступные для перехода состояния

### TicketStateListener
_**TicketStateListener**_ — это сервис для отправки тикетов на отслеживание изменения их состояний.
- %%(java)void listen(StartrekTicket ticket)%% — начать отслеживать тикет (положить его ключ и текущее состояние в базу).

### TicketStateTransitionProcessor
_**TicketStateTransitionProcessor**_ — По сути, этот сервис нужен только для того, что бы вызывать его из тмс-таски. Он будет проверять, не изменилось ли состояние какого-либо из тикетов, лежащих в базе. Если изменилось, то будет триггерить `TicketTransitionHandler`, соответствующий новому состоянию тикета.
- %%(java)void processAll()%% — достать все незакрытые тикеты из базы, проверить, не поменялось ли их состояние и, при необходимости, обновить его, потриггерив соответствующие хэндлеры. Будет дёргаться из ТМС.

## Как использовать у себя?
Для начала нужно определиться, какой именно функционал нужен. Есть 2 варианта конфигурации
- `StartrekServiceOnlyConfiguration` — если нужно просто создавать и манипулировать тикетами (без отслеживания их состояния)
- `StartrekModuleFullConfiguration` — если нужен полный модуль (манипуляция с тикетами + отслеживание)

**В итоге нужно подключать 3 или 4 конфига:**
В **главный конфиг и тесты** подключаем
- `StartrekServiceOnlyConfiguration` или `StartrekModuleFullConfiguration`

Только в главный:
- `StartrekExternalConfiguration`

Только в тесты:
- `StartrekExternalMocksConfiguration`
- `StartrekListenerTestClassesConfiguration` — если нужно. Содержит тестовые фабрики для `TicketState`, подключать только вместе с `StartrekModuleFullConfiguration`

Так же, нужно не забыть добавить в проперти oauth-токен робота для доступа к стартреку.
`tpl.tracker.oauth=...`

### А что в базе?
Если подключать полный модуль, то ещё понадобится добавить такой скрипт в ликвибейз (см. актуальный в `market-tpl/pvz/pvz-core/src/liquibase/table/ticket/ticket_state.sql`):
```sql
--liquibase formatted sql

--changeset denr01:ticket_state
CREATE TABLE IF NOT EXISTS ticket_state
(
    key        TEXT        NOT NULL PRIMARY KEY,
    status     TEXT        NOT NULL,
    opened     BOOLEAN     NOT NULL DEFAULT TRUE,

    created_at TIMESTAMPTZ NOT NULL,
    updated_at TIMESTAMPTZ NOT NULL
);

CREATE INDEX idx_st_ticket_is_closed ON ticket_state (opened);

--changeset denr01:ticket_state_comments runOnChange:true
COMMENT ON TABLE ticket_state IS 'Отслеживаемые startrek-тикеты';
COMMENT ON COLUMN ticket_state.key IS 'Ключ тикета';
COMMENT ON COLUMN ticket_state.status IS 'Послдний известный статус тикета';
COMMENT ON COLUMN ticket_state.opened IS 'Открыт/Закрыт';
```

Сущности для хибера подтянутся автоматически при подключении полного конфига.

### Как работать со своей очередью?
Для начала, нужно её добавить в `TicketQueueType`.
В принципе, это необходимый минимум.

Если предполагается использование каких-то новых полей, нужно добавить их в `TicketField`.

Если нужно менять состояния тикета, то их нужно описать в отдельном енуме, который будет реализовывать `TicketStatusEnum`. Для примера можно посмотреть `QuickStartWorkflowStatus` в тестах самого модуля.

Если понадобилось менять статусы, то, скорее всего, понадобится и работать с резолюциями. Их описываем аналогичным статусам образом, только реализуем интерфейс `TicketResolutionEnum`. Пример можно посмотреть в `QuickStartWorkflowResolution` там же, где и пример со статусами.

### Как отслеживать переходы состояний в своей очереди?
1) Убедиться, что подключен полный модуль, а не service-only (см. выше).
2) Добавить скрипт в ликвибейз, что бы создалась табличка в базе.
3) Добавить TMS-таску, аналогичную `FetchStartrekTicketsExecutor`, в которой будет вызываться `ticketStateTransitionProcessor.processAll();` раз в определённый интервал.
4) Для интересующих тикетов вызывать `ticketStateListener.listen(ticket);`.
5) Создать хэндлеры для интересующих состояний (реализовать `TicketTransitionHandler`), в котором указать тип очереди, к которой относятся интересующие тикеты, состояние, при переходе в которое хэндлер будет вызываться, а так же сами действия, которые должны в этот момент происходить. Над каждым хэндлером нужно навесить аннотацию `@Component`, что бы обработчик переходов их увидел.
