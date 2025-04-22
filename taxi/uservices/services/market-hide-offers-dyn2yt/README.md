# Market Hide-Offers Dynamic To YT Сonverter Service

## Описание

Микросервис скрытий позволяет <b>конвертировать входные "динамик" файлы в унифицированный файл скрытий</b> в формате ```.mmap```.

<br>

Функционально сервис работает следующим образом:
- скачиватся входные динамики
- конвертируются в выходный файл скрытий
- выгружаются в s3-mds bucket (основной и запасной, только мастер делает этот шаг)

Поддержанные динамики:
- [abo](https://a.yandex-team.ru/arc_vcs/market/library/unified_hide_rule/lib/converters)
- [shop-cpa](https://a.yandex-team.ru/arc_vcs/market/library/unified_hide_rule/lib/converters) # WIP
- [shop-cpc](https://a.yandex-team.ru/arc_vcs/market/library/unified_hide_rule/lib/converters) # WIP
- [shop-supplier](https://a.yandex-team.ru/arc_vcs/market/library/unified_hide_rule/lib/converters)

Графики:
 - [production](https://monitoring.yandex-team.ru/projects/market-hide-offers/dashboards/monu786jshn11r8vb899?from=now-1d&to=now&refresh=60000)
 - [testing](https://monitoring.yandex-team.ru/projects/market-hide-offers/dashboards/mon1mrlth09q48ne3igq?from=now-1d&to=now&refresh=60000)

<br>

## Архитектура

### Конвейер обработки
```
  Input files                                  Microservice                                   Output files
+-------------+       +-------------------------------------------------------------+
| Dynamic 1   |  -->  |                                                             |
+-------------+       | +---------------+     +-------------+                       |
                      | | Periodic-task | --> | File 1      |     +---------------+ |
                      | |  (dynamic 1)  |     |             | <-- | Periodic-task | |       +---------------+
                      | +---------------+     +-------------+     |  (s3 upload)  | |       | S3-MDS bucket |
      ...             |        ...                  ....          |               | |  -->  |               |
                      | +---------------+     +-------------+     |               | |       |               |
                      | | Periodic-task | --> | File N      | <-- |               | |       +---------------+
                      | |  (dynamic N)  |     |             |     +---------------+ |
+-------------+       | +---------------+     +-------------+                       |
| Dynamic N   |  -->  |                                                             |
+-------------+       +-------------------------------------------------------------+

```

### Master-Slave

```
               +-------------+
               |             |
               |  Distlock   |
               |             |
               +-------------+
                /           \
+-------------------+  +-------------------+
| Instance 1        |  | Instance 2        |
| Master            |  | Slave             |
| - collect dynamic |  | - collect dynamic |
| - process dynamic |  | - process dynamic |
| - upload dynamic  |  |                   |
+-------------------+  +-------------------+
```

<br>

## Как разрабатывать микросервис?

### Cредствами ya make
```
cd arcadia/taxi/uservices/services/market-hide-offers-dyn2yt
ya make # cборка
ya make -tt # сборка + тесты
```

### Cредствами taxi make
Для сборки сервиса использовать:
```
cd arcadia/taxi/uservices
make build-[SERVICE-NAME]
```

Для тестирования сервиса использовать:
```
cd arcadia/taxi/uservices
make test-[SERVICE-NAME]
make utest-[SERVICE-NAME]
make testsuite-[SERVICE-NAME]
```

Для форматирования исходного кода использовать:
```
cd arcadia/taxi/uservices/services/
taxi-format market-hide-offers-dyn2yt/
```
---
**NOTE:**
Для этой команды используйте Docker образ!

---

Если вы добавили новые библиотеки то необходимо перегенрировать сборочные файлы:
```
cd arcadia/taxi/uservices
make gen-[SERVICE-NAME]
```
---
**NOTE:**
Для этой команды используйте Docker образ!

---

<br>

## Docker образ

1. Вы можете ознакомится с деталями поддержки Docker в [задаче](https://st.yandex-team.ru/MARKETOUT-46028).
2. [Dockerfile](https://st.yandex-team.ru/ajax/v2/attachments/52415349)
3. [docker-run.sh](https://st.yandex-team.ru/ajax/v2/attachments/58176820)
4. [docker-build.sh](https://st.yandex-team.ru/ajax/v2/attachments/52415348)

<br>

## Как подключиться к микросервису?

* через интерфейс [nanny](https://nanny.yandex-team.ru/ui/#/services) выбрать окружение (production/testing)
* у работающего сервиса скопировать доменное имя, например ```vqqikvqgockuwejz.man.yp-c.yandex.net```
* подключиться по ```ssh```

<br>

## Полезные статьи:

1. [Taxi admin](https://tariff-editor.taxi.yandex-team.ru/services/152/edit/356462/info)
2. [S3 buckets-production](https://yc.yandex-team.ru/folders/akuue7eoga29bp44vb1a/storage/buckets)
3. [S3 buckets-testing](https://yc-test.yandex-team.ru/folders/akuue7eoga29bp44vb1a/storage/buckets/offers-dyn2yt-tst)
4. [Документация](https://wiki.yandex-team.ru/users/vlmarkov/minimarket-hide-offers-microservice/)
5. [Дежурства](https://wiki.yandex-team.ru/users/vlmarkov/minimarket-hide-offers-microservice/minimarket-hide-offers-microservice-duty-instruction/)
6. [Корневая задача](https://st.yandex-team.ru/MINIMARKET-4)
