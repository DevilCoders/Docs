# model-params
Model params servantlet

Выкладка релиза через ЦУМ [здесь](https://tsum.yandex-team.ru/pipe/projects/pers/delivery-dashboard/market-pers-model-params "Выкладка через CD")

Nanny [dashboard](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_pers_model_params "dashboard")

### RTC

[Nanny](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_pers_model_params)

Секреты для запуска сервиса разделяются c pers-history
- [тест](https://yav.yandex-team.ru/secret/sec-01f33rxm53bmjp5bvwzer2755h/explore/versions)
- [прод](https://yav.yandex-team.ru/secret/sec-01f33rzp2vkw49as35y0kqryq9/explore/versions)

После изменения секрета можно накатить его через `persec history test/prod`

### Сборка и запуск 

Сборка и прогон тестов `ya make -tt`

Локальный запуск - через класс `ModelParamsMain`
Переменные окружения
```
ENVIRONMENT=local
```

JVM args
```
-Dlog4j.configurationFile=/home/$USER/arc/arcadia/market/pers/model-params/src/main/conf/local/log4j2-test.xml
```


