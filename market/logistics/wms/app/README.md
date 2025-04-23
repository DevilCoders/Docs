## Локальный запуск

0. Установить JDK версии, указанной [тут](https://a.yandex-team.ru/arc/trunk/arcadia/market/logistics/wms/app/ya.dependency_version.inc#L2)
    - из [Аркадии](https://docs.yandex-team.ru/ya-make/manual/java/#prerequisites-ustanovka-arkadijnoj-jdk) (команду нужно немного адаптировать к JDK17:
    ```cd arcadia/jdk && ya make -DJDK_VERSION=17 && mkdir ~/jdk-17 && tar xf jdk17.tar -C ~/jdk-17```), добавить JDK в IDEA: `File → Project Structure → Platform Settings → SDKs -> "+" → Add JDK...`
    - из IDEA: `File → Project Structure → Platform Settings → SDKs → "+" → Download JDK...`
    - из репозитория вашей OS. Для macos можно использовать brew: `brew install --cask temurin`

    При установке не из Аркадии надо [добавить](https://wiki.yandex-team.ru/security/ssl/sslclientfix/#macosx) в JDK сертификаты Яндекса:
    После этого добавляем JDK в IDEA: File → Project Structure → Project Settings → SDK, устанавливаем в этом поле "17".

1. Генерация проекта для IntelliJ Idea `ya ide idea --yt-store --directory-based --group-modules=flat --generate-junit-run-configurations -r $(pwd) -l $(pwd)` (да, можно прям в томй же папке оставлять, в принципе все будет работать)
2. Поднять inforDB (mssql), nginx (балансер UI -> все сервисы), postgres итд.. `cd dependency-stubs && docker-compose up -d` (нужно быть [авторизованным](https://wiki.yandex-team.ru/qloud/docker-registry/#authorization) в docker-registry)
3. Нужно добавить недостающие проперти
  - достать содержимое файла из секрета https://yav.yandex-team.ru/secret/sec-01fnb2byegrdbp0t4wm69wbxt7/explore/version/ver-01g11d7dhvhan77p6ng957b0xk
  - или скопировать файл с пропертями [отсюда](https://arcanum.yandex-team.ru/arc/trunk/arcadia/market/sre/conf/wms-init/properties/common.properties) или заполненные со стенда (например с `wms-app01vp.market.yandex.net` `sudo cat /etc/yandex/datasources/infor/application.properties`) с любого стенда
  - положить локально так же в `/etc/yandex/datasources/infor/application.properties` или завести файлик  `application-development.properties` внутри приложения.
4. Логи по-умолчанию приложение пишет в `/var/log...` Если этого не хочется, то можно в `application-development.properties` указать `logging.config` на файл с конфигом logback, чтобы логи отправлять только в консоль (см `conf/local/logback-spring.xml`)


## Сервисы

| Сервис  | Порт  | Debug  | URL |
|---|---|---|---|
|  OLTP |  8080, 8081 | 8788  |
|  BATCH | - |  8791 |
|  UI |  8110 |   8790 |
|  SocketServer | -  |  7000 |
| | | | |
|  Api | 6666  |   |  /api |
|  Auth | 8392  |   |  /auth |
|  Autostart | 1488  |   |  /autostart |
|  Consolidation | 4488  |   |  /consolidation |
|  Constraints | 8366 | /constraints |
|  Core | 8333  |  | /core |
|  DataCreator | 8599 | | datacreator |
|  Dimension Management | 8340 | | /dimensionmanagement |
|  Dropping | 7777  |   | /dropping |
|  Inbound Management | 8300 | | /inbound-management |
|  Inventorization | 8377 |  | /inventorization |
|  Inventory Management | 8311 |  | /inventory-management |
|  OrderManagement | 8765  |  | /ordermanagement |
|  Packing |  8182 |   | /packing2 |
|  Picking | 2488  |   |  /picking |
|  Placement |  8388 |   | /placement |
|  Receiving | 8282 | | /receiving |
|  Replenishment | 19100  |  | /replenishment |
|  Reporter | 8390  |  | /reporter |
|  Scheduler | 8388  |  | /scheduler |
|  ServiceBus | 8382  |   | /servicebus |
|  Shipping | 7070 | | /shipping |
|  Shippingsorter | 8240  | 8241 | /shippingsorter |
|  Task Router | 8399 | | /taskrouter |
|  Transportation | 8238  |   |  /transportation |
|  WCS Emulator | 8600 | | /wcs-emulator |
| Palletizer | 8345 | | /palletizer |

