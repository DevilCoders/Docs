# TVM auth client

Библиотека для работы с [tvm](https://wiki.yandex-team.ru/passport/tvm2/)

Примеры использования можно посмотреть [здесь](example_test.go)

Есть две реализации:
- tvmtool (стандартная для работы через tvmtool)
- tvmauth (имплементация с зависимостью от CGO и без tvmtool)

Имеет готовый набор инструментов для работы с [Service Ticket](https://wiki.yandex-team.ru/passport/tvm2/theory/) по
grpc: [пример](example_grpc_test.go)

Работа с [User Ticket](https://wiki.yandex-team.ru/passport/tvm2/user-ticket/) на данный момент не поддерживается (будет
реализована в [VOID-603](https://st.yandex-team.ru/VOID-603))

## tvmtool

Реализация с использованием tvmtool, он же [tvm-daemon](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/)
Сам tvmtool обычно кладётся в контейнер с приложением

## tvmauth

Реализация с использованием CGO, использует "экзотическую" криптографию как модуль OpenSSL, оторвано от аркадии.

- для сборки требуется libssl-dev (есть в наших build-образах golang начиная с 1.16.12 и 1.17.5)
- для запуска требует glibc (привет, alpine)
