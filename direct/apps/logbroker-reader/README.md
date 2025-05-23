# logbroker-reader - консольная утилита для чтения из LogBroker 

Читает сообщения из LogBroker и выводит их на stdout.

По своей сути является копией [kikimr/persqueue/binaries/cli](https://a.yandex-team.ru/arc/trunk/arcadia/kikimr/persqueue/binaries/cli/main.cpp) со следующими отличиями:
- добавлена возможность ограничить количество вычитываемых сообщений
- оторвана возможность записи в LogBroker
- аутентификация по OAuth-токенам заменена на TVM с чтением секрета из файле
- преднастроена на престейбл-логброкера и соответсвующие TVM-секреты

Предоставляется без каких-либо гарантий и строго НЕ для использования в продакшн.

## Как пользоваться
1. Собрать: `ya make`
2. Запустить: `./lb read -s logbroker-pre.yandex.net -t direct-test--access-log -l 10`, где:
  - `direct-test--access-log` - имя топика который читаем
  - `10` количество сообщений, после которых завершаем чтение

Сообщений может быть вычитано больше лимита
Клиент будет ждать сообщения, если топик вычитан до конца

## tail -f на топик
Если указать опцию `-n` и не указывать лимит `-l`, то утилита будет вычитывать из топика все незакомиченные данные, и не будет коммитить вычитанное.
real-time просмотр логов ставок `./lb read -s logbroker-pre.yandex.net -n -t direct-test--direct-ppclog-price-log`
