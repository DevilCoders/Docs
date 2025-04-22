### pers-grade-admin-view-x5

#### Как посмотреть логи?
Заходим на logview
```
ssh logview.market.yandex.net
```
Монтируем логи для сервиса(пункт Nanny сервисы)
```
varvara@logview01ed:~$ mount-service-log testing_market_front_pers_grade_admin_vla
/mnt/nanny/testing_market_front_pers_grade_admin_vla/30318@vla1-4584.search.yandex.net has been mounted
```
Что можно смотреть?
```
varvara@logview01ed:~$ ls /mnt/nanny/testing_market_front_pers_grade_admin_vla/30318@vla1-4584.search.yandex.net
    nginx        xscript           xscript.log.2.gz
    push-client  xscript.log.1.gz  xscript.log.3.gz
```

#### Ex-волшебные порты или noxsl-выдача
##### Тестинг: https://admin-pers-testing-noxsl.market.fslb.yandex.ru/
##### Прод: https://admin-pers-stable-noxsl.market.fslb.yandex.ru/

#### [Пайплайн в ЦУМе](https://tsum.yandex-team.ru/pipe/projects/pers/release/new/market-pers-grade-admin-view)
#### [Таска в TeamCity из мастера](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Market_Abo_Pers_PersGrade_PersGradeAdminViewRtc)
#### [Sandbox ресурс](https://sandbox.yandex-team.ru/resources/?type=MARKET_PERS_GRADE_ADMIN_VIEW)
#### Nanny сервисы
[Дашборд в Nanny](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_pers_grade_admin/)

[Сервис в Nanny для pers-grade-admin-view(прод, Ивантеевка)](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_front_pers_grade_admin_iva/)

[Сервис в Nanny для pers-grade-admin-view(прод, Владимир)](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_front_pers_grade_admin_vla/)

[Сервис в Nanny для pers-grade-admin-view(прод, Сасово)](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_front_pers_grade_admin_sas/)

[Сервис в Nanny для pers-grade-admin-view(тестинг, Сасово)](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_front_pers_grade_admin_sas/)

[Сервис в Nanny для pers-grade-admin-view(тестинг, Владимир)](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_front_pers_grade_admin_vla/)


#### Запуск дева
Может быть запущена на derkoat. Для этого нужно в домашней директории создать директорию ```www/pers-grade-admin-view``` и положить туда (вручную или с помощью системы контроля версий) исходники. Затем в этой же директории нужно создать файл ```ns.xml``` с описанием бекендов (за основу можно взять ```ns-testing.xml``` или ```ns-production.xml```, которые лежат в репозитории). После этого компонент будет доступен по адресу вида ```https://pers-grade-admin-view.<login>.user.derkoat.yandex.ru```.
Нацелить компонент на нужные бекенды можно, указав их в файле ```ns.xml``` (например, таким образом можно протестировать связку из dev-бекенда на braavos и dev-фронтенда на derkoat).
