Как запустить из-под среды разработки (на примере Intellij Idea)

В локальном файлике с настройками `app-local.properties` указать требуемые параметры для легковесной конфигурации.
Параметры легковесной конфигурации можно подсмотреть в файле app-development.properties (секция Lightweight).

Затем в IDE создать конфигурацию для запуска Bidding со следующими параметрами

Working dir:

`полный-путь-до-модуля/src/script` чтобы приложение нашло файлы с конфигами.

Main Class:

`ru.yandex.market.bidding.Main`

VM options:
```
-ea
-Doracle.net.tns_admin=/etc/oracle
-Dconfigs.path=../main/properties.d
-Denvironment=local
-Dspring.profiles.active=development,shop
-Dbidding.debug=yes
-Dbidding.intern=yes
-Dbidding.buffer=no
-Xmx2048m
-Xms1024m
-XX:+UseG1GC
-XX:+UseStringDeduplication
-XX:-OmitStackTraceInFastThrow
```

где

 - `ea` - включить assertions (помогает отловить баги на ранней стадии)
 - `oracle.net.tns_admin` - путь к папке с файлом tnsnames.ora
 - `bidding.debug` - полезно для отладки приложения (см. класс Globals)
 - `bidding.intern` - включить интернирование строк (пул строк)
 - `bidding.buffer` - включение/отключение пула буферов обработки рез-в примения ставок
 - `UseStringDeduplication` - включить дедубликацию строк
 - `OmitStackTraceInFastThrow` - полезно для распечатки стека в любом случае, т.е. не использовать fast stack

В `app-local.properties` также следует перекрыть JDBC-параметры соединения
```
shops_web.billing.jdbc.driverClassName=oracle.jdbc.driver.OracleDriver
shops_web.billing.jdbc.url=jdbc:oracle:thin:@billing-dev
shops_web.billing.username=shops_web
shops_web.billing.password=SHOPS_WEB
```

Запустить и смотреть лог mbi-bidding.log
Для загрузки какого-нибудь магазина в кеш нужно выполнить одну из сервисных операций Bidding API по магазину.
Например, http :3870/market/bidding/774/groups (использую тулзу HTTPie из-за ее дружелюбности по сравнению с curl)

При запуске из-под IDE могут возникнуть конфликты в версиях по бибилиотекам. Например, это возникает для библиотеки
Jackson, которая  идет с версией 2.2.0 в checkout-common и 2.6.0 в mbi-bidding-common. Последняя версия является верной
для Bidding, но связывается в IDE версия 2.2.0 по непонятным причинам. В этом случае нужно просто удалить jar-файлы
с неверной версией из списка External Libraries->IvyIDEA-mbi-bidding (см. Project View).

Зависимости между проектами для работы и запуска Bidding в IDE, включая отладку (см. Project Structure->Module Dependencies):

- mbi-common IvyIDEA (export)
- checkout-common IvyIDEA (export)
- checkouter-client -> checkout-common, IvyIDEA
- push-api-client -> checkout-common, checkouter-client, IvyIDEA
- mbi-core -> mbi-common, IvyIDEA (export), checkout-common, checkouter-client, push-api-client, shopadmin-stub-client
- mbi-bidding-common -> mbi-core, IvyIDEA (export)
- mbi-bidding -> IvyIDEA, mbi-bidding-common, mbi-core
