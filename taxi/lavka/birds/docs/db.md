# Работа с БД

## Миграции

*   Для миграций используется [pgmigrate](https://github.com/yandex/pgmigrate)
*   Исходники миграций хранятся в директории `services/<name>/postgresql/<name>/migrations` (важно для pgmigrate)
*   Для запуска миграций в `testing/production` окружении нужно

    *   Зайти в соответствующее окружение tariff-editor на вкладку:

        * [unstable](https://tariff-editor.taxi.dev.yandex-team.ru/dev/scripts)
        * [testing](https://tariff-editor.taxi.tst.yandex-team.ru/dev/scripts)
        * [production](https://tariff-editor.taxi.yandex-team.ru/dev/scripts)

        ```
        Для анстейбла нужно убедиться, что tariff-editor работает в режиме api анстейбла
        ```
    
        * В боковом меню под надписью unstable должно быть написано `api-u`
        * Если написано `api-t`, то нужно нажать на надпись, чтобы переключиться в режим api unstable
        
    *   Создать новый скрипт:

        * [pigeon](../services/pigeon/docs/db.md#novyj-skript-pgmigrate)
        * [falcon](../services/lavka-falcon/docs/db.md#novyj-skript-pgmigrate)
        * [eagle](../services/eagle/docs/db.md#novyj-skript-pgmigrate)

    Если требуется запустить миграцию из определенной ветки (например для PR), то к аргументам необходимо добавить:

    ```
    --branch=<длинный id коммита, например, 936b6508a36589846a8dd7a7725d2234c014adb7>
    --forked_by=<название ветки, например, users/p-nemykin/EAGLE-315>
    ```
   
    *   **(production only)** Тикет в очереди [TAXIBACKEND](https://st.yandex-team.ru/TAXIBACKEND)
    *   В описании изменений часто пишут лишь номер ревизии миграции
    *   Для `testing / unstable` скрипт подтверждается самостоятельно

    Подробнее в [инструкции](https://wiki.yandex-team.ru/taxi/backend/taxi-tech/zapusk-skriptov/#zapuskpgmigrate)

    *   Откат миграции происходит путём написания новой миграции

---

## Запуск произвольных SQL скриптов

*   Добавляем скрипты в проект [tools-py3](https://a.yandex-team.ru/arcadia/taxi/infra/tools-py3/) в соответсвующей папке:

    * [pigeon](https://a.yandex-team.ru/arcadia/taxi/infra/tools-py3/lavka_pigeon)
    * [eagle](https://a.yandex-team.ru/arcadia/taxi/infra/tools-py3/lavka_eagle)
    * [falcon](https://a.yandex-team.ru/arcadia/taxi/infra/tools-py3/lavka_lavka-falcon)

*   **Важный момент:** к скриптам мы добавляем `BEGIN;` и `COMMIT;`. Это нужно для того, чтобы если что-то пойдет не так, скрипт автоматически откатился	
*   Пример [скрипта](https://a.yandex-team.ru/arcadia/taxi/infra/tools-py3/lavka_eagle/sql/V001-weight-db.sql)	

*   Зайти в соответствующее окружение tariff-editor:

    * [production](https://tariff-editor.taxi.yandex-team.ru/dev/scripts)	
    * [testing](https://tariff-editor.taxi.tst.yandex-team.ru/dev/scripts)
    * [unstable](https://tariff-editor.taxi.dev.yandex-team.ru/dev/scripts)

* Создать новый скрипт:

    * [pigeon](../services/pigeon/docs/db.md#novyj-skript-sql)
    * [falcon](../services/lavka-falcon/docs/db.md#novyj-skript-sql)
    * [eagle](../services/eagle/docs/db.md#novyj-skript-sql)

*   **(production only)** Тикет в очереди [TAXIBACKEND](https://st.yandex-team.ru/TAXIBACKEND)
*   В описании изменений часто пишут лишь номер ревизии миграции
*   Для `testing / unstable` скрипт подтверждается самостоятельно

---

## ReadOnly доступ

Если у RO пользователя не хватает прав на `SELECT`

`SQL Error [42501]: ERROR: permission denied for table...`

Необходимо зайти на облачный инстанс приложения и выполнить команду:

```bash
PGSSLMODE=require \
psql -U taxi -d pigeon -p 6432 -h <host> \
    -c 'GRANT SELECT ON ALL TABLES IN SCHEMA public TO taxiro' \
    -c 'GRANT SELECT ON ALL SEQUENCES IN SCHEMA public TO taxiro' \
    -c 'GRANT SELECT ON ALL TABLES IN SCHEMA catalog TO taxiro' \
    -c 'GRANT SELECT ON ALL SEQUENCES IN SCHEMA catalog TO taxiro'
```

Пароль и хосты можно найти на инстансе (`cat /etc/yandex/taxi-secdist/taxi.json`)
