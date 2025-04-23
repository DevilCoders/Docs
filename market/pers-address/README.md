# pers-address
Address presets and suggests for Market Front Applications
[чат поддержки](https://t.me/joinchat/ChXJS0uvDnKNwdWfgQS8DA)

# Выкладка
[Автоматическая в ЦУМе](https://tsum.yandex-team.ru/pipe/projects/pers/delivery-dashboard/pers-address-arc-pipeline)

# Балансеры

## testing
Адрес: http://pers-address.tst.vs.market.yandex.net:80

Тикет в CSADMIN: https://st.yandex-team.ru/CSADMIN-22950

## production
Адрес: http://pers-address.vs.market.yandex-team.ru:80

Тикет в CSADMIN: https://st.yandex-team.ru/CSADMIN-22951

## prestable(load)
Адрес: http://pers-address-prestable.vs.market.yandex.net:80

Тикет в CSADMIN: https://st.yandex-team.ru/CSADMIN-27132, https://st.yandex-team.ru/CSADMIN-27283

# Инфраструктура

[Сервис в Сасово, тестинг](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_pers_address_sas/)

[Сервис в Сасово, прод](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_pers_address_sas/)

[Сервис в Ивантеевке, прод](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_pers_address_iva/)

[Сервис во Владимире, прод](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_pers_address_vla/)

# Мониторинги
[Гафики в Графане (прод и тестинг)](https://grafana.yandex-team.ru/d/BpVmJZvmk/pers-address-dashboad?orgId=1)

# Swagger
[Описание API - Swagger UI](http://pers-address.tst.vs.market.yandex.net/swagger-ui.html)

Если не открывается закажите доступы в [панчере](https://puncher.yandex-team.ru/)

# База
## Тестинг
[yc](https://yc.yandex-team.ru/folders/foo4b5i8ioau23qpc3bu/managed-postgresql/cluster/a98e090a-05c5-46ce-ab1a-2c5520bbe2ff)

[solomon](https://solomon.yandex-team.ru/?project=internal-mdb&cluster=mdb_a98e090a-05c5-46ce-ab1a-2c5520bbe2ff&service=mdb&dashboard=internal-mdb-cluster-postgres)

[golovan](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=a98e090a-05c5-46ce-ab1a-2c5520bbe2ff;dbname=market_loyalty_quiz_testing?range=86400000)

## Прод
[yc](https://yc.yandex-team.ru/folders/foo4b5i8ioau23qpc3bu/managed-postgresql/cluster/0a051740-5862-429b-811e-ce3859d3eccb)

[solomon](https://solomon.yandex-team.ru/?project=internal-mdb&cluster=mdb_0a051740-5862-429b-811e-ce3859d3eccb&service=mdb&dashboard=internal-mdb-cluster-postgres)

[golovan](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=0a051740-5862-429b-811e-ce3859d3eccb;dbname=market_loyalty_quiz_prod?range=86400000)

**обновление dependencies.lock**
```bash
find . -name 'dependencies.lock' | xargs rm
./gradlew clean :pers-address-db:generateLock :pers-address-db:saveLock :pers-address-back:generateLock :pers-address-back:saveLock
```

Поддерживаются следующие ключи:
```
-Plocal -Pinmem -Ptms
```
