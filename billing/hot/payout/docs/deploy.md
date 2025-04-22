# Проект

https://deploy.yandex-team.ru/projects/billing-payout

# Сетевые макросы

- Балансеры:
    - `_BILLING_AWACS_PAYOUT_TEST_NETS_`
    - `_BILLING_AWACS_PAYOUT_PROD_NETS_`

- Серванты:
    - `_BILLING_DEPLOY_PAYOUT_TEST_NETS_`
    - `_BILLING_DEPLOY_PAYOUT_PROD_NETS_`

# TVM

- Прод:
    - api: 2025546
    - tasks: 2025550

- Тест:
    - api: 2025542
    - tasks: 2025544

Вот тут все можно посмотреть:

- https://abc.yandex-team.ru/services/newbillingpayout/resources/?supplier=14&type=47&type=50&state=requested&state=approved&state=granting&state=granted&view=consuming

# Как собирается проект

Проект собирается через Arcadia CI. Сборка описана тут:

- https://a.yandex-team.ru/arc/trunk/arcadia/billing/hot/payout/a.yaml

Результатом сборки являются docker-образы:

- `balance/billing-payout`
- `balance/billing-payout-req-gate`
- `balance/billing-payout-oebs-gate`

# Переменные окружения

## Системные

- `PAYOUT_CONFIG` - путь к конфигу
- `PAYOUT_TVM_SRC` - TVM Id тек. компонента
- `PAYOUT_TVM_ALLOWED` - список TVM, которым разрешено к нам ходить
- `PAYOUT_ACCOUNTS_URL` - URL для системы счетов
- `PAYOUT_ACCOUNTS_TVM` - TVM системы счетов
- `PAYOUT_CPF_URL` - URL старого баланса (api для создания cash-payment-fact)
- `PAYOUT_CPF_TVM` - TVM баланса
- `PAYOUT_CPF_URL_DRY_RUN` - URL нашей ручки, имитирующей старый баланс
- `PAYOUT_CPF_TVM_DRY_RUN` - TVM нашей ручки, имитирующей старый баланс
- `PAYOUT_LB_OEBS_BASE_PATH` - базовый путь для топиков ОЕБС
- `PAYOUT_LB_NOTIFIER_BASE_PATH` - базовый путь для нотификационных топиков
- `PAYOUT_LB_OEBS_ERRORS_BASE_PATH` - базовый путь для топика с ошибками OEBS
- `PAYOUT_SENDER_LIMIT` - размер пачки для обработки новых выплат
- `PAYOUT_OEBS_GATE_INTERVAL` - интервал опроса БД для новых выплат
- `PAYOUT_REQUEST_LIMIT` - размер пачки для обработки новых заявок
- `PAYOUT_REQ_GATE_INTERVAL` - интервал опроса БД для новых заявок
- `PAYOUT_DB_HOSTS` - список хостов, где крутится БД
- `PAYOUT_DB_PASSWORD` - пароль для БД

## Флаги

- `PAYOUT_SYNC_CPF` - включение синхронизации cash-payment-fact
- `PAYOUT_HTTP_CPF_SENDER` - включение отправки cash-payment-fact в Баланс через синхронную HTTP ручку
- `PAYOUT_LOGBROKER_CPF_SENDER` - включение отправки cash-payment-fact в Logbroker асинхронно
- `PAYOUT_PROCESS_DRY_RUN` - включение обработки признака dry_run (по умолчанию включен)
- `PAYOUT_EMULATE_OEBS` - включает эмуляцию ответов из OEBS в компоненте tasks
- `PAYOUT_MONITORING_PAYOUT_RETRO_TIME` - кол-во дней, за которые мы смотрим статистику по `t_payout`. Остальное берем
  из `mv_payout`, которая пере собирается раз в сутки. Сделали, чтобы не сканировать все партиции `t_payout`. Относится
  к `retardation` метрикам. Значение по умолчанию - 7.
- `PAYOUT_MONITORING_PAYOUT_MAX_AGE` - кол-во дней, за которые мы смотрим статистику по измененным платежам. Сделали,
  чтобы не сканировать все партиции `t_payout`. Относится к `sliced_*` метрикам. Значение по умолчанию - 7.
- `PAYOUT_APPROVE_REQUIRED` - список `namespace`, по которым будет проставляться признак ручного подтвержения выплаты.
  Ставится в DU `req-gate`. Пример:
  `PAYOUT_APPROVE_REQUIRED=["bnpl"]`. Если выставить значение `"global"`, то будет для всех активно.
  Задача: https://st.yandex-team.ru/BILLING-679
- `PAYOUT_ALLOWED_NS` - список клиентов для каждого `namespace`, для которых будут доступны настоящие выплаты (
  не `dry-run`). Ставится в DU `oebs-gate`. Для остальных клиентов настоящие выплаты будут отклоняться. Если
  какого-то `namespace` нет, то для него ограничений не будет.
  Пример: `PAYOUT_ALLOWED_NS={"taxi": [123, 456], "oplata": []}`:
    - для `taxi` обрабатываем настоящие выплаты только по клиентам 123 и 456, остальные реджектим
    - для `oplata` реджектим все настоящие выплаты
    - для любого другого встретившегося `namespace` обрабатываем все настоящие выплаты
    - задача: https://st.yandex-team.ru/BILLING-677
- `PAYOUT_LB_ENDPOINT`/`PAYOUT_LB_PORT` - позволяют задать подключение к логброкеру. НЕ ИСПОЛЬЗОВАТЬ В ПРОДАКШЕНЕ. Нужно
  только для рецептов

# Релизы

Релизы собираются через Arcadia CI:

- https://a.yandex-team.ru/projects/newbillingpayout

Конфиг:

- https://a.yandex-team.ru/arc/trunk/arcadia/billing/hot/payout/a.yaml

# Логи

Через push-client все логи грузятся в YT:

- Прод:
    - https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/billing-payout-payout-prod-api
    - https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/billing-payout-payout-prod-tasks

- Тест:
    - https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/billing-payout-payout-test-api
    - https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/billing-payout-payout-test-tasks
