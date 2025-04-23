# Сервис Биллинга Маркета

## Локальный запуск приложения

0. Для работы с проектом нужно установить Java и Kotlin.
1. Поднять локальную базу Postgres. Можно воспользоваться образом в докере
    - Можно воспользоваться файлом
      [docker-compose.yml](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/docker-compose.yml);
    - Вызвать команду `docker-compose up` из корня проекта.
2. В консоле локальной базы выполнить команды
   из [скрипта](https://a.yandex-team.ru/arc_vcs/market/billing/db/src/liquibase/local/init.sql), если
   роли еще не были созданы. Для запуска tms команд нужно создать qrtz таблицы в локальной базе, для этого выполнить
   команды
   из [следующих файлов](https://a.yandex-team.ru/arc_vcs/market/billing/db/src/liquibase/local/).
   Например так `PGPASSWORD=*** psql -h localhost -p 5432 -U market_billing_dev -d market_billing_dev < init.sql`
   (реквизиты доступа можно взять в `liquibaseDev.sh` или `docker-compose.yml`)
3. Запустить `./liquibaseDev.sh` (может понадобится установить requests, например через `pip3 install requests`)
4. Выполнить из директории проекта команду `python3 downloadProps.py`.
Может возникнуть ошибка:
```
{
   "code": "error",
   "message": "No keys in the SSH Agent. Check output of 'ssh-add -l' command"
}
 ```
   В таком случае необходимо выполнить команду `ssh-add` из папки `~/.ssh`.
5. В созданном файле `src/main/properties.d/development/00_local.properties`
   дописать в пустую пропертю  yql-токен, который можно получить в настройках YQL.
   За juggler-токеном, если он действительно необходим, обратиться к [voznyuk-da](https://staff.yandex-team.ru/voznyuk-da)

6. Добавить в VM-options следующие настройки для запуска (**проверье пути до проектов IDEA и до Аркадии**!!)
  ```
    -Djava.library.path=$HOME/IdeaProjects/arcadia-market_billing_market-billing-tms/dlls
    -Djna.library.path=$HOME/IdeaProjects/arcadia-market_billing_market-billing-tms/dlls
    -Denvironment=development
    -Dlog4j2.contextSelector=org.apache.logging.log4j.core.async.AsyncLoggerContextSelector
    -Dlog.dir=/tmp
    -Dconfigs.path=$HOME/arc/arcadia/market/billing/market-billing-tms/src/main/properties.d
    -Dlog4j.configurationFile=$HOME/arc/arcadia/market/billing/market-billing-tms/src/main/conf/local/log4j2-test.xml
    -Dspring.profiles.active=development
    --enable-preview
  ```
Если хотите локально включить работу GOE необходимо добавить профиль `goe-processing`.
Таким образом, предпоследняя строка принимает вид `-Dspring.profiles.active=development,goe-processing`

