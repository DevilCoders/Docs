# pers-history

статус сборки [![Build Status](http://teamcity.yandex-team.ru/app/rest/builds/buildType:Market_Abo_Pers_PersHistory/statusIcon)](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Market_Abo_Pers_PersHistory)

### Описание 

История просмотров пользователя

[Страница на Wiki](https://wiki.yandex-team.ru/market/development/pers/history/)

[Памятка дежурному](https://wiki.yandex-team.ru/market/development/pers/duty/)

[Памятка разработчику](https://wiki.yandex-team.ru/users/varvara/market/development/pers/)

[API (тестинг)](http://pers-history.tst.vs.market.yandex.net:38602/swagger-ui.html)

### Выкладка

[Релиз из транка](https://tsum.yandex-team.ru/pipe/projects/pers/delivery-dashboard/pers-history-arc)

[Выкладка в тестинг из ветки](https://tsum.yandex-team.ru/pipe/projects/pers/release/new/pers-history-arc-branch)

Проверку доработок желательно делать до вливания в транк - через выкатку из бранчи.
Нужно указывать путь пользовательской ветки в арке `users/user_name/branch_name` или `trunk` для выкатки из транка.

При выкатке релиза из транка нужно зайти в релизную машину, и из неё запустить релиз нужной ревизии.

### RTC

[Nanny](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_pers_history/)

Логи в ```logs/pers-history/pers-history.log```

Секретница:
- [тест](https://yav.yandex-team.ru/secret/sec-01f33rxm53bmjp5bvwzer2755h/explore/versions)
- [прод](https://yav.yandex-team.ru/secret/sec-01f33rzp2vkw49as35y0kqryq9/explore/versions)

После изменения секрета можно накатить его через `persec history test/prod`

### Графики сервиса

[Solomon](https://solomon.yandex-team.ru/admin/projects/market-pers-history)

[Grafana](https://grafana.yandex-team.ru/d/000001548/pers-history?orgId=1)

[nginx](https://yasm.yandex-team.ru/template/panel/market-nginx/itype=marketpershistory;ctype=production;prj=market?range=7200000)

[proto метрики](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketpershistory;ctype=production;prj=market)

### Графики БД views

[тестинг](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=3e6d54fb-bd61-455c-a4cb-81fa7ec16699;dbname=pers_views_testing)

[прод](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=33c65295-9b63-44ba-b9b7-6b7abbe12e92;dbname=pers_views_production)

### Управление базами

[Управление тестовой mysql](https://yc.yandex-team.ru/folders/fooqc51fitontalf6vjl/managed-mysql/cluster/mdbt770pcg4g8peb843p)

[Управление продовой mysql](https://yc.yandex-team.ru/folders/fooqc51fitontalf6vjl/managed-mysql/cluster/mdbbimtg07ltmhkt5kk2)

### Сборка и запуск 

Сборка и прогон тестов `ya make -tt`

Локальный запуск можно сделать напрямую и через скрипт. Подробности в [документации](https://wiki.yandex-team.ru/users/ilyakis/maret-java-arcadia-migration/#lokalnyjjzapusk)

[Локальный сваггер](http://localhost:8080/swagger-ui.html)

#### Локальный запуск через скрипт
Запуск приложения
```
# простой запуск
./local-start.sh

# в режиме отладки
./local-start.sh --debug-port=6666
```

#### Локальный запуск напрямую
Локальный запуск - через класс `PersHistoryMain`
Переменные окружения
```
ENVIRONMENT=local
```

JMV args
```
# если хочется, чтобы логи выводились в консоль
-Dlog4j.configurationFile=/home/#USER/arc/arcadia/market/pers/static/src/main/conf/local/log4j2-test.xml
```
