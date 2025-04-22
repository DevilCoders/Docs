# Как выполнять отладку partner-api в среде DEV

Для DEV-среды можно использовать машину **braavos**.

## Сборка приложения

```
ya make
```

## Выкладка приложения на сервер

```$xslt
../uploadToDev.sh partner-api
```

### Настройка TNS

tnsnames.ora привозится через etcd в /etc/oracle/tnsnames.ora (https://github.yandex-team.ru/cs-admin/datasources-ng-dev).
Если вдруг захочется указать другой tnsnames.ora, то можно переопределить параметр запуска **-Doracle.net.tns_admin**
в файле src/main/properties.d/00.servant-local.properties в свойстве environmentJvmArgs

### Настройка параметров приложения
Настроить приложение перед выкладкой можно в файле src/main/properties.d/development/servant-development.properties

Рекомендуемые настройки:

```
http.host=<EXTERNAL_HOST_NAME>
http.port=<HTTP_PORT>
```
Так же можно указать **debug.port**.
Выбранные порты не должны конфликтовать с другими пользователями.
Проще всего это сделать, если выбирать порты из зарезервированных за пользователем (см. соотв-щую викистраницу).

Опциональные настройки, если хочется использовать зависимые компоненты из QA-ландшафта:

```
# memcache-сервера
memcached.server.list.global=mbi1ft:11212

# Javasec
java_sec.billing.http.proxy.url=http://mbi1ft:34798/

# Bidding (ставки)
market.bidding.url=https://mbiddingha.market.yandex.net:38700/market/bidding

# Bidding развернутый локально
#market.bidding.url=http://localhost:3870/market/bidding/

# Credentials для доступа к Bidding по HTTPS (BASIC auth с проксированием https через nginx)
market.bidding.security.username=bidding-client
market.bidding.security.password=Sheet9eib2IXai9o

# Репорт
market.search.maxcpms.url=http://mslb01ht.market.yandex.net:8742/yandsearch
market.click.search.url=http://mclick-report.yandex.net:38610/yandsearch
market.search.url=http://msh01ht.market.yandex.net:17051/yandsearch

# Чекаутер
market.checkouter.client.url=http://gravicapa1ft:39001/

# к балансу
balance.xmlrpc.serverUrl=http://xmlrpc.balance.greed-ts1f.yandex.ru:8002/xmlrpc

#Подключение к тестовому ClickHouse
mbi.clickhouse.jdbc.db=mbi
mbi.clickhouse.jdbc.password=/*достать из пропертей для тестинга*/
mbi.clickhouse.jdbc.url=jdbc:clickhouse://sas-ei7q3v1257mlagbx.db.yandex.net:8443,vla-tm1ivrepn95w6u9j.db.yandex.net:8443

#заглушка mds
market.mds.s3.path=http://nowhere.com/
```

В случае развертывания собственной версии компоненты в DEV нужно использовать ее адрес в данном конфиге.

В случае использования базы Биллинга в QA нужно перекрыть соотв-щие параметры приложения для JDBC-соединения.

Для этого надо смотреть параметры приложений Маркета в *datasources.properties* для *testing*.

## Запуск приложения

```
bin/partner-api-start.sh
tailf logs/market-partner-api.log
```

Если в логе все хорошо, то можно приступить к отладке. Для этого надо прокинуть тунель на бравос, например:
ssh -L port:127.0.0.1:hostport braavos.market.yandex.net
использовать адрес 127.0.0.1:<DEBUG_PORT>.

## Полезные советы

 - Запросы к Partner API без OAuth можно выполнить используя http-хедер **X-AuthorizationService: Mock** и куку ***yandexuid=23708286**.
