nuvault
=======

Не замысловатый сервис по обмену хостового (выписанного на `YandexInternalRootCA`) сертификата на секретик.
На текущий момент конфигурится исключительно статическим [конфигом](https://a.yandex-team.ru/arc/trunk/arcadia/security/gideon/nuvault/deploy/cfg.yaml), ибо не предполагает массового (т.е. широким кругом лиц) использования.

Логика работы
=============

Что касается серверной части:
  - раз в `sync_period` ходит в YAV за новыми версиями секретов
  - реализует gRPC API ([спека](https://a.yandex-team.ru/arc/trunk/arcadia/security/gideon/nuvault/pkg/nuvrpc/service.proto)) с mutual authentication
  - при запросе секрета чекает, что клиент аутентфицировался правильным сертом и если это так - отдает последнюю версию секрета

Что касается клиентской части:
  - клиент ходит в endpoint set `nuvault.Api` (живет в `sas`, `vla`, `man` и `iva`)
  - аутентифицируется сертом
  - дергает ручку `NuVaultService.GetSecret`, которая по UUID секрета вовзращает его содержимое (все его ключи)
  - реализация Go клиента: https://a.yandex-team.ru/arc/trunk/arcadia/security/gideon/nuvault/pkg/nuvault
  - дока к нему: https://godoc.yandex-team.ru/pkg/a.yandex-team.ru/security/gideon/nuvault/pkg/nuvault/
  - минимальный пример: https://a.yandex-team.ru/arc/trunk/arcadia/security/gideon/nuvault/pkg/nuvault/nuvault_example_test.go

How to
======
 Как добавить новый секрет:
  1. выдать роботу [robot-gideon](https://staff.yandex-team.ru/robot-gideon)  доступ на чтение нужного секретика
  2. добавить его в конфиг
  3. пнуть buglloc@ чтоб выкатил
