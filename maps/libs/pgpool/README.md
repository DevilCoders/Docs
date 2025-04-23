# pgpool library

Библиотека предназначена для управления пулом соединений к Постгресу на стороне клиента.

Основные возможности:
* возможность создания транзакций на чтение/запись к мастеру на чтение к репликам
* кэш соединений
* многопоточная работа
* автоматическое определение мастера
* автоматическое определение ближайшей реплики

## Getting started

Добавьте заголовочные файлы:

```cpp
#include <maps/libs/pgpool/include/pgpool3.h>
```

Создайте конфигурацию - список хостов, входящих в кластер.

```cpp
pgpool3::InstanceId master("master.maps.yandex.ru", 5432);
pgpool3::InstanceId slave1("slave1.maps.yandex.ru", 5432);
pgpool3::InstanceId slave2("slave2.maps.yandex.ru", 5432);

pgpool3::PoolConfiguration configuration(master, {slave1, slave2})
```

Создайте строку соединения без хоста и порта:

```cpp
std::string connParams = "dbname=my_db user=my_name password=my_password";
```

Задайте параметры работы пула:

```cpp
auto constants = pgpool3::PoolConstants::create(
    10, //master connection count
    20, //max master connection count
    10, //slave connection count
    20); //max slave connection count
```

Теперь всё готово для создания пула:

```cpp
pgpool3::Pool pool(
    std::move(configuration),
    std::move(connParams),
    std::move(constants));
```

Пример использования:

```cpp
auto txn = pool.masterWriteableTransaction();
txn->exec("INSERT INTO table (field1, field2, field3) VALUES (1, 2, 3)");
txn->commit();
```

## Pool initialization

### Pool initialization from XML-config

Класс `maps::pgp3utils::DynamicPoolHolder` позволяет проинициализировать пул целиком из XML-конфига.

Пример XML-конфига:

```xml
<database name="mapspro">
    <write host="master.maps.yandex.ru" port="5432"/>
    <read host="slave1.maps.yandex.ru" port="5432"/>
    <read host="slave2.maps.yandex.ru" port="5432"/>
    <pool writePoolSize="4"
        writePoolOverflow="4"
        readPoolSize="6"
        readPoolOverflow="9"
        timeout="1"
        pingPeriod="30"/>
</database>
```

Пример инициализации:

```cpp
auto doc = xml3::Doc::fromFile("config.xml");

maps::pgp3utils::DynamicPoolHolder holder(doc.node("/config/database"));

auto txn = holder.pool().masterWriteableTransaction();
```

Ниже подробнее рассмотрена инициализация пула в ручном режиме.

### pgpool3::PoolConfiguration

pgpool должен знать, какие хосты (инстансы) входят в кластер.

* Можно указать явно, какой инстанс является мастером, а какие - репликами, если вы уверены, что роли инстансов никогда не поменяются.
* Можно указать просто список инстансов. pgpool сам определит, кто их них является мастером, а кто репликами.

Пример задания конфигурации в виде списка инстансов:

```cpp
pgpool3::PoolConfiguration configuration({
    pgpool3::InstanceId("host1.maps.yandex.ru", 5432),
    pgpool3::InstanceId("host2.maps.yandex.ru", 5432),
    pgpool3::InstanceId("host3.maps.yandex.ru", 5432)
})
```

Также список инстансов можно хранить в виде XML-конфига:

```cpp
const std::string CONFIG =
R"(<database name="mapspro">
    <write host="master.maps.yandex.ru" port="5432/>
    <read host="slave1.maps.yandex.ru" port="5432"/>
    <read host="slave2.maps.yandex.ru" port="5432""/>
</database>)";

auto doc = xml3::Doc::fromString(CONFIG);

pgpool3::PoolConfiguration configuration(doc.root());
```

### Connection parameters

Это строка соединения в формате `key=value`, но без указания хоста и порта.
Обязательные параметры: `dbname`, `user`, `password`.
Полный список параметров: https://www.postgresql.org/docs/9.6/libpq-connect.html#LIBPQ-PARAMKEYWORDS

Пример:

```cpp
std::string connParams = "dbname=my_db user=my_name password=my_password";
```

### pgpool3::PoolConstants

TODO:

| Constant name | Default value | Description |
| ------- | ------- | ------- |
| masterSize | - | Количество соединений к мастеру, которые будут поддерживаться открытыми по крайней мере `freeConnectionIfIdleForMs` миллисекунд |
| masterMaxSize | - | Максимально возможное количество соединений к мастеру. Если это количество больше `masterSize`, то избыточные соединения будут жить по крайней мере `excessConnectionsDecayMs` миллисекунд |
| slaveSize | - | Количество соединений к одной реплике, которые будут поддерживаться открытыми по крайней мере `freeConnectionIfIdleForMs` миллисекунд |
| slaveMaxSize | - | Максимально возможное количество соединений к одной реплике. Если это количество больше `slaveSize`, то избыточные соединения будут жить по крайней мере `excessConnectionsDecayMs` миллисекунд |
| connectionUsageLimit | 5000 | Если в соединении было создано это количество транзакций, то оно закрывается. 0 - нет лимита на количество транзакций |
| freeConnectionIfIdleForMs | 15min | Если соединение не используется дольше этого времени, то оно закрывается. 0 - соединение живёт бесконечного долго |
| excessConnectionsDecayMs | 10s | Если соединение не используется дольше этого времени, и имеется избыток соединений, то оно закрывается |
| getTimeoutMs | 1s | Максимальное время ожидания соединения при взятии транзакции |
| pingIntervalMs | 30s | Интервал между пингами одного хоста |
| pingTimeoutMs | 5s | Если не удается подключиться к хосту дольше этого времени, то хост будет считаться неактивным (offline) |
| tokenCacheSizePerInstance | 10000 |  |
| waitForTokenOnSlaves | 0.2 |  |
| instancesToCheckTokenFactor | 0.2 |  |
| tokenCheckIntervalMs | 1s |  |
| waitForAvailabilityInfo | true | Блокировать выполнение конструктора пула, пока от всех хостов не будет получен результат пинга |
| timeoutEarlyOnMasterUnavailable | true |  |
| maxConnectionAttempts | 1 |  |
| treatMasterAsSlave | false | Разрешить использование автоматически определённого мастера в том числе и в режиме реплики для слейв-запросов даже при наличии других реплик. Работает и имеет смысл только в случае, если хосты были заданы без явного указания ролей |

### Logging

pgpool активно логирует свои действия и позволяет перенаправлять сообщения лога с помощью объекта-логгера.
Для этого нужно создать класс-логгер, который наследуется от `pgpool3::logging::Logger`,
и передать его в специальный конструктор пула:

```cpp
pgpool3::Pool pool(
    std::make_shared<CustomLogger>(),
    std::move(configuration),
    std::move(connParams),
    std::move(constants));
```

По умолчанию, pgpool использует класс `pgpool3::logging::MapsLogAdapter`,
который перенаправляет сообщения в библиотеку `maps/libs/log8`.

## Pool usage

pgpool под капотом поддерживает пул соединений с базой данных:
открывает новые соединения при необходимости,
закрывает старые, если они долго не используются.

Чтобы начать отправлять запросы в БД нужна транзакция - объект класса `pgpool3::TransactionHandle`,
который является обёрткой над `pqxx::transaction_base`.

Для получения транзакции используются методы класса `Pool`:

```cpp
TransactionHandle Pool::masterWriteableTransaction()
TransactionHandle Pool::masterReadOnlyTransaction()
TransactionHandle Pool::slaveTransaction(const std::string& token = std::string{})
```

Первые 2 метода создают транзакцию к мастеру. 3й метод - транзакцию к реплике.
Если создать транзакцию к реплике по какой-то причине не возможно, то берётся транзакция к мастеру.
Если опция treatMasterAsSlave имеет значение true, то 3-й метод может создавать транзакции к мастеру наравне с другими репликами.

Вызов этих методов приводит к захвату соединения из пула.
Если в пуле нет свободных соединений, то создаётся новое соединение.
Если количество соединений достигло лимита (`masterMaxSize` или `slaveMaxSize`), то pgpool ждёт,
пока какое-нибудь соединение не освободится. Время ожидания ограничено параметром `getTimeoutMs`.
Если время ожидания истекло, то кидается исключение `pgpool3::Timeout`.

Соединение удерживается до момента уничтожения объекта `TransactionHandle`.
Досрочно освободить соединение можно вызовом метода:

```cpp
TransactionHandle::releaseConnection();
```

Не рекомендуется удерживать соединение, если транзакция больше не используется.

Делать запросы можно напрямую через объект `TransactionHandle` с помощью оператора `->`:

```cpp
auto txn = pool.masterWriteableTransaction();
txn->exec("INSERT INTO table (field1, field2, field3) VALUES (1, 2, 3)");
txn->commit();
```

Либо можно получить ссылку на `pqxx::transaction_base`:

```cpp
auto txn = pool.masterWriteableTransaction();
pqxx::transaction_base& pqxxTxn = *txn;
```

Метод `masterWriteableTransaction` создаёт `pqxx::transaction`.
Все изменения, сделанные в этой транзакции, не будут видны другим транзакциям,
пока не вызыван метод `commit`.
Если не был вызван `commit` или в процессе возникла ошибка, то все изменения в базе данных будут откачены.

Методы `masterReadOnlyTransaction` и `slaveTransaction` создают `pqxx::read_transaction`.
Последующие запросы увидят изменения в соответствии с настроенным transaction isolation level.

## Pool internals

TODO:

## Communication with 3rd party services

### DBaaS

При инициализации конфигурации нужно указать список хостов, полученный через DBaaS API.
DBaaS гарантирует, что имена хостов не поменяются.

В строке соединения нужно указать `sslmode=verify-full`:

```cpp
std::string connParams = "dbname=my_db user=my_name password=my_password sslmode=verify-full";
```

При этом нужно положить SSL-сертификат в файл `~/.postgresql/root.crt` в домашней директории пользователя,
из-под которого запущен процесс. Подробнее в официальной документации.

Сертификат можно найти в Аркадии: https://a.yandex-team.ru/arc/trunk/arcadia/certs/yandex_internal.pem

В докер-образ можно положить через pkg.json:

```
{
    "source": {
        "type": "ARCADIA",
        "path": "certs/yandex_internal.pem"
    },
    "destination": {
        "path": "/install/<homedir>/.postgresql/root.crt",
        "attributes": {
            "mode": {
                "value": "0600"
            }
        }
    }
}
```

В Картах `<homedir>` может принимать значения:

* `/var/www` - для yacare-сервисов, которые работают из-под пользователя `www-data`
* `/home/maps` - для фоновых процессов, которые работают из-под пользователя `maps`

Нужно установить режим работы менеджера подключений **SESSION**:

```
yc managed-postgresql cluster update --id <clusterId> --connection-pooling-mode SESSION
```

Официальная документация: https://doc.yandex-team.ru/cloud/mdb/

## Getting pgpool state and statistics

TODO:

## Replication tokens

TODO:

## pgpool internals

TODO: Выбор ближайшей реплики. Балансировка

### Caveats

TODO: Нет защиты от записи в readonly-транзакциях

TODO: Исчерпание соединений к репликам

### Pinger

TODO: Как работает пингер
