## Утилита для заполнения агрегатной проверки на основе графа Nirvana

```
./generate_monthclose_alert \
    --workflow-instance-id='b4772be3-31df-4829-92b1-94fc32e2b939' \
    --nirvana-token-filename=./nirvana_token \
    --juggler-token-filename=./juggler_token \
    --alert-service-prefix='payplatform.financial_month_closing.task_' \
    --alert-host='financial_month_closing' \
    --aggregate-host='financial_month_closing' \
    --aggregate-service='payplatform.financial_month_closing.aggregate'
```

## Параметры
- `--workflow-instance-id='b4772be3-31df-4829-92b1-94fc32e2b939'` – Идентификатор Workflow Instance, из которого брать список вершин.
- `--nirvana-token-filename=./nirvana_token` – OAuth токен для Nirvana.
- `--juggler-token-filename=./juggler_token` – OAuth токен для Juggler.
- `--alert-service-prefix='payplatform.financial_month_closing.task_'` – префикс сервиса алертов, должен совпадать с указанным в операции Get Nirvana Task Statuses.
- `--alert-host='financial_month_closing'` – хост алертов, должен совпадать с указанным в операции Send Juggler Raw Events
- `--aggregate-host='financial_month_closing'` – хост агрегатной проверки, должен совпадать с указанным в агрегатной проверке, на которую будут созданы оповещения.
- `--aggregate-service='payplatform.financial_month_closing.aggregate'` – сервис агрегатной проверки, должен совпадать с указанным в агрегатной проверке, на которую будут созданы оповещения.
