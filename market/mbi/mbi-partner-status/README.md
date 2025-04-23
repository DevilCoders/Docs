### Скорее всего это не тот partner-status который вы ищите.
Скорее всего вам сюда:
https://a.yandex-team.ru/arcadia/market/mbi/partner-status

### Локальный запуск без TVM

1. Postgres
   ```
   mkdir -p $HOME/docker/volumes/postgres
   docker run --name mbi_partner_status -e POSTGRES_PASSWORD=mbi_partner_status -e POSTGRES_USER=mbi_partner_status -h localhost -p 5432:5432 -d postgres
   ```
1. Запускаем ``ru.yandex.market.javaframework.main.ApplicationMain`` в IDEA через main

### Локальный запуск с TVM

1. Postgres (как в пред. пункте)
1. Добавить VM-options для запуска приложения
   ```
   -Dmbi.partner_tvm.tvm2.enabled=true
   ```
1. Добавляем client_id и секрет от tvm. ``client_secret`` и ``market.mbi.partner.status.tvm.client.id``. Секреты можно найти в
   секретнице
   ```
   client_id
   market.mbi.partner.status.tvm.client.id=

   Тестинг: 2025490
   Прод: 2025492
   ```
   Секретница: [тестинг](https://yav.yandex-team.ru/secret/sec-01et4r81j32pn5y9h90fstyt0n/explore/version/head)
   , [прод](https://yav.yandex-team.ru/secret/sec-01et4r8q899yzna6ssxwknhbtv/explore/version/head)
1. Запускаем ``ru.yandex.market.javaframework.main.ApplicationMain`` в IDEA через main
