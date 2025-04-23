Библиотек для работы с [ErrorBooster](https://wiki.yandex-team.ru/error-booster/). Инструкция по подключению к ErrorBooster: [тут](https://wiki.yandex-team.ru/error-booster/error-how-to/#kakpodkljuchitsja).

# Sentry
В данный момент реализован `SentryTransport`, с помощью которого можно настроить отправку событий [sentry](https://a.yandex-team.ru/arc/trunk/arcadia/vendor/github.com/getsentry/sentry-go) в [ErrorBooster](https://wiki.yandex-team.ru/error-booster/). [Код с примером](https://a.yandex-team.ru/arc/trunk/arcadia/noc/go/errorbooster/examples/simple/example.go).

# Важно, используйте с пониманием!
Текущая реализация сделана блокирующей, т.е. для подлежащего LB можно задать лимит по используемой памяти:
* если этот лимит исчерпан — отправка событий будет заблокирована до освобождения памяти
* если лимит не задан (что является дефолтным поведением) - начнёт расти расход памяти, пока не съест всю
