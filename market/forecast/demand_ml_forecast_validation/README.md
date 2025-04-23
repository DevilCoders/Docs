# Инфра для прогноза спроса

#run

run.sh --mode (prod|dev|dev_sampled) --command (validate|predict)

## CI/CD

- [Project]
- [Reaction]
- [Stage]
    - 2d9cdeb6-d4ab-4439-b875-88aa6b0b0c35
- [Stable]
    - 45513b02-604b-4461-b491-67e88207bd1c
- [Prod]
    - 027a9074-db00-4163-80c6-48eb91ab59b0

[project]: https://nirvana.yandex-team.ru/browse?selected=9063387
[reaction]: https://reactor.yandex-team.ru/browse/resolve?path=%2Fhome%2Frobot-replenishment%2FWorkflows%2Fdemand_ml_forecast%2Fdemand-ml-forecast-ci-prod-run-0.1
[stage]: https://nirvana.yandex-team.ru/browse?selected=9063390
[stable]: https://nirvana.yandex-team.ru/browse?selected=9063389
[prod]: https://nirvana.yandex-team.ru/browse?selected=9063388

## Требования к коду

### Все таски создаются через task/tasks/ForecastTask
Обязательно указывать при создании таски параметр:
key_fields = ['msku', 'forecast_date'] - список ключей по которым проверяются дубли.
Таска после выполнения будет проверять в выходной таблице(result_path) наличие дублей.
Если в таблице есть дубли кубик упадёт и будет сообщение в логе о наличии дублей.

