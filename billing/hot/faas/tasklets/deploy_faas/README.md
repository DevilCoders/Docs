# Тасклет Deploy Faas

## Описание
Тасклет деплоит [faas бинари](https://a.yandex-team.ru/arc/trunk/arcadia/billing/hot/faas/python), сгенерированные sdk2 таской [BillingFaasBuild](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/billing/tasks/Faas/BillingFaasBuildTask) в Деплой.

## Как обновить
1. `make sb-upload`
2. Обновить id ресурса здесь: https://a.yandex-team.ru/arc/trunk/arcadia/ci/registry/projects/billing/billing_faas_deploy.yaml
3. Обновить https://a.yandex-team.ru/arc/trunk/arcadia/billing/hot/manificenta/a.yaml (пока не сойдется https://st.yandex-team.ru/CI-933)
