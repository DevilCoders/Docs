# Гайд "Что делать при просадке денег?"

В чат дежурств иногда приходят с проблемами просадки денег -- за какой-то продукт стали списывать заметно меньше.
Этот гайд предназначен помочь в локализации и решении проблемы.

## Дашборд обилливания

Для начала нужно ответить на вопрос "В какой части биллинга проблема?". Для этого есть [дашборд в графане](https://grafana.vertis.yandex-team.ru/d/uPWbq517z/billing-events-handling).

Сверху дашборда есть настраиваемые переменные:
- **datasource** -- выбор между продом и тестингом.
- **domain** -- домен (aka service_name).
- **kafka_topic** -- топик сырых событий.
- **window** и **timing_window** -- размер окна для группировки метрик на графиках.

У каждого графика есть описание на русском, доступное по подсказке в верхнем левом углу графика.

## Этапы обилливания событий

Весь процесс обилливания разбит на 5 этапов.

#### 1) Чтение сырых событий из кафки.
   - [Описание этапа](../notes/consuming_kafka.md)
   - На [дашборде обилливания](#дашборд-обилливания) соответствующие графики собраны в ряд  _"Consuming raw events from kafka"_

#### 2) Формирование обилленных событий (списаний) из сырых событий.
   - [Описание работы со звонками](https://a.yandex-team.ru/arcadia/classifieds/verticals-backend/billing/billing/billing-tms/logic/src/tasks/CallsStatisticsUpdateTask.scala#L20-L30?rev=r9253252)
   - [Описание работы с событиями indexing](https://a.yandex-team.ru/arcadia/classifieds/verticals-backend/billing/billing/billing-tms/logic/src/tasks/IndexingToCampaignEventsTask.scala#L25-L34?rev=r9253252)
   - На [дашборде обилливания](#дашборд-обилливания) соответствующие графики собраны в ряд _"Raw events -> CampaignEvents"_

#### 3) Создание транзакций из обилленых событий.
   - [Описание этапа](https://a.yandex-team.ru/arcadia/classifieds/verticals-backend/billing/billing/billing-tms/logic/src/tasks/WithdrawFormTask.scala#L19-L28?rev=r9253252)
   - На [дашборде обилливания](#дашборд-обилливания) соответствующие графики собраны в ряд _"CampaignEvents -> transactions"_

#### 4) Отправка транзакций в брокер (yt).
   - [Описание этапа](https://a.yandex-team.ru/arcadia/classifieds/verticals-backend/billing/billing/billing-tms/logic/src/tasks/BillingOperationPushTask.scala#L41-L55?rev=r9253252)
   - На [дашборде обилливания](#дашборд-обилливания) соответствующие графики собраны в ряд _"Transactions -> yt"_

#### 5) Отправка списаний в Баланс.
   - [Описание этапа](https://a.yandex-team.ru/arcadia/classifieds/verticals-backend/billing/billing/billing-tms/logic/src/tasks/BalanceSyncTask.scala#L18-L24?rev=r9253252)
   - На [дашборде обилливания](#дашборд-обилливания) соответствующие графики собраны в ряд _"Transactions -> Balance"_

## Вспомогательные вещи

Кроме того есть другие полезные гайды:
- Гайд ["Отслеживание события в стораджах биллинга"](track_billing_events.md)
- [Примеры запросов статистики списаний в mysql и yt](statistics_queries.md)

Посмотреть на верхнеуровневые схемы обилливания событий можно [в записях tech-talk](https://wiki.yandex-team.ru/vertis/billing/tech-talks/):
- Запись _"2021-01-20 Обилливание событий с типом Indexing"_
- Запись _"2021-11-17 Рассказ про обилливание звонков"_
