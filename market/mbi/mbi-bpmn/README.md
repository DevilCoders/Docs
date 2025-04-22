### Договоренности по сохранению истории процессов

1. Уровень сохранения истории (**History level**) устанавливаемым в значение ``audit``, так как при ``full`` слишком
   много ненужной информации.
1. При создании нового процесса ``historyTimeToLive`` устанавливаем в стандартное значение ``P14D``. По истечение 14
   дней, информация по процессу будет удлаена из таблиц.

### Локальный запуск без TVM

1. Postgres
   ```
   mkdir -p $HOME/docker/volumes/postgres
   docker run --name mbi_bpmn -e POSTGRES_PASSWORD=mbi_bpmn -e POSTGRES_USER=mbi_bpmn -h localhost -p 5432:5432 -d postgres
   ```
1. Запускаем ``ru.yandex.market.mbi.bpmn.MbiBpmn`` в IDEA через main

### Локальный запуск с TVM

1. Postgres (как в пред. пункте)
1. Добавить VM-options для запуска приложения
   ```
   -Dmbi.partner_tvm.tvm2.enabled=true
   ```
1. Добавляем client_id и секрет от tvm. ``client_secret`` и ``market.mbi.bpmn.tvm.client.id``. Секреты можно найти в
   секретнице
   ```
   client_id
   market.mbi.bpmn.tvm.client.id=

   Тестинг: 2025490
   Прод: 2025492
   ```
   Секретница: [тестинг](https://yav.yandex-team.ru/secret/sec-01et4r81j32pn5y9h90fstyt0n/explore/version/head)
   , [прод](https://yav.yandex-team.ru/secret/sec-01et4r8q899yzna6ssxwknhbtv/explore/version/head)
1. Запускаем ``ru.yandex.market.mbi.bpmn.MbiBpmn`` в IDEA через main
