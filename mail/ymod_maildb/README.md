# Что
Модуль для корректного создания `macs::Service`

# Зачем
Для использования `macs_pg` нужно написать некоторое количество кода: инициализации `user_journal`, обвязки для `sharpei_client`, создание `UidResolver`, etc. Этот код одинаковый для разных сервисов. Не писать его нельзя: `macs_pg` зависит от `sharpei_client` и `user_journal`. Можно получить объект `macs::Service` без журнала пользователя, но это не будет правильно: все модифицирующие операции должны попадать в `user_journal.tskv` и литься в Yt. Модуль позволяет переиспользовать код и легко получить `macs::Service`

# Как устроено
Интерфейс модуля:
```cpp
struct Module {
    virtual user_journal::ServicePtr userJournalService() const = 0;
    virtual user_journal::Uatraits uatraits() const = 0;
    virtual user_journal::Geobase geobase() const = 0;

    virtual macs::ServicePtr service(const ServiceParams& params,
                                     const UserJournalParams& uj,
                                     macs::pg::logging::v2::LogPtr macsPgLog,
                                     const pgg::QueryHandleStrategy& strategy) const = 0;

    user_journal::Journal journal(const ServiceParams& s,
                                  const UserJournalParams& uj) const;
};
```

Для создания сервайза или журнала нужно инициализировать структуры:
* `ymod_maildb::ServiceParams` - данные о пользователе, запросе и опциональные: тип пользователя, учетные данные для доступа к базе
* `ymod_maildb::UserJournalParams` - данные для записи в `user_journal.tskv`: эксперименты, тип устройства, yandexuid, etc

В библиотеке есть хелперы для создания этих структур из `ymod_webserver::response`: `ymod_maildb::parseServiceParams` и `ymod_maildb::parseUserJournalParams`

Для создания экземпляра журнала этих стркутур будет достаточно. Для сервайза нужно дополнительно передать логгер и стратегию запросов

# Конфигурирование
Пример конфигурации:
```yaml
-   _name: sharpei_client
system:
    name: sharpei_client
    factory: yhttp::cluster_client
configuration:
    hosts: http://sharpei-testing.mail.yandex.net:80
    reactor: global
    retry_policy:
        max_attempts: 2
        split_timeout: true
    default_request_timeout: 0.6s
-   _name: maildb
    system:
        name: maildb
        factory: ymod_maildb::MacsPgWithUserJournal
    configuration:
        dependencies:
            reactor: global
        logger:
            module: example
            user_journal_errors: example
            user_journal: journal
        user_journal:
            table_name: users_history
            write_chunk_size: 100
            write_poll_timeout_ms: 500
            locale: ''
            tskv_format: mail-user-journal-tskv-log
        metadata:
            sharpei:
                http_client:
                    cluster_client_module: sharpei_client
            pg:
                query_conf: query.conf
                user: web
                connection_pool:
                    connect_timeout_ms: 500
                    queue_timeout_ms: 100
                    query_timeout_ms: 60000
                    max_connections: 9
                    fail_threshold: 0
                transaction_timeout_ms: 600000
        geodata_path: /var/cache/geobase/geodata5.bin
        uatraits:
            config: /usr/share/uatraits/browser.xml
            profiles: /usr/share/uatraits/profiles.xml
        corp: false
```

На данный момент есть только одна реализация интерфейса модуля: `ymod_maildb::MacsPgWithUserJournal`. Она должна быть указана в `system.factory`

## Секция `configuration`
Узел `dependencies` содержит зависимости модуля:
* `dependencies.reactor` опциональная зависимость. Реактор нужен для выполнения запросов в базу данных и для клиента шарпея

Если `dependencies.reactor` пустой, то:
* для нужд `sharpei_client` будет использован `yplatform::global_net_reactor->io()`
* для `macs_pg` будет создан `boost::asio::io_service` с числом тредов, равным `metadata.pg.connection_pool.workers_count`

Если `dependencies.reactor` не пустой, то из реактора будет взят `boost::asio::io_context` и прокинут в `sharpei_client` и `macs_pg`. Если реактора с таким именем не существует, то будет выброшено исключение

### Важно
Часто реакторам задают конфигурацию "много io_context с одним тредом": `{ _name: global, _io_threads: 1, _pool_count: 10 }`. В таком случае в `sharpei_client` и `macs_pg` попадёт `io_service` с **одним** тредом

Больше информации:

* https://a.yandex-team.ru/arc/trunk/arcadia/mail/ymod_maildb/module.cc?rev=r8262979#L106
* https://a.yandex-team.ru/arc/trunk/arcadia/mail/yplatform/lib/reactor/reactor.cc?rev=r7588791#L99
* https://a.yandex-team.ru/arc/trunk/arcadia/mail/yplatform/lib/reactor/reactor.cc?rev=r7946824#L87


Узел `logger` содержит информацию о логировании:
* `module` - служебный логер, в который пишется информация о загрузке ymod_maildb::MacsPgWithUserJournal
* `user_journal_errors` - логер для ошибок журнала пользователя
* `user_journal` - логер для журнала событий. Обычно этот файл сразу грузят в Yt

Узлы `user_journal` и `metadata` конфигурируют библиотеки `user_journal` и `macs_pg` соответственно
* `metadata.sharpei.http_client`: это нужно для походов в шарпей, см. документацию [sharpei_client](https://a.yandex-team.ru/arc/trunk/arcadia/mail/sharpei_client) для конфигурирования.

Булевое значение `corp` нужно для репозитория настроек

Настройки `geobase` и `uatraits.*` нужны для инициализации [хелперов для user_journal](https://a.yandex-team.ru/arc/trunk/arcadia/mail/user_journal/helpers?rev=r6919310)
* `geodata_path` - путь до файла с геодатой
* `uatraits.config` и `uatraits.profile` - пусть до конфигов uatraits

Все три поля могут быть `null`. Тогда создадутся дефолтные врапперы для `geobase` и `uatraits`. Это применяется в тестах чтоб не тащить тяжёлые файлы в тестовую среду


# Примеры
Лежат в папке [example](https://a.yandex-team.ru/arc/trunk/arcadia/mail/ymod_maildb/example?rev=r8075790)
