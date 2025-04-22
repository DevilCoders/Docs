# Маркет для Бизнеса - офис

## Настройка проекта

1. Выполните generate_project.sh . После этого в ~/projects/b2b-office будет сгенерирован проект для Idea.
2. Открываем проект:
  - File -> Project structure -> Project -> Project SDK указываем 17 версию. Если в списке нет 17 версией, то
    нажимаем Edit и Add JDK.. Указываем путь полученный с помощью `ya tool java17 --print-path` (без `/bin/java`)

    ###### Для запуска тестов:
  - Run -> Edit configurations -> Edit configuration templates -> JUnit -> Add VM options добавляем ```--add-opens=java.base/java.lang=ALL-UNNAMED -Duser.timezone=Europe/Moscow -Duser.language=en```

    ###### Для локального запуска приложения:
  - Run -> Edit configurations -> Add -> Application
    - VM options добавляем ```--add-opens=java.base/java.lang=ALL-UNNAMED -Duser.timezone=Europe/Moscow -Duser.language=en``` и ```-Dconfigs.path=/home/tesseract/arcadia/market/b2b/office/application/src/main/properties.d```
    - Class path of module указываем ```b2boffice```
    - Main class указываем ```ru.yandex.market.b2b.office.Server```
3. Добавляем конфигурацию TVM.
Для этого в ```application/src/main/conf/local/tvm-local.json``` кладем содержимое [TVM_SECRET_JSON](https://yav.yandex-team.ru/secret/sec-01g3ztnbja6pje9wyyenv62a5m/explore/versions)
4. Скопировать ```log4j2.template.xml``` в ```log4j2.xml``` в директории ```application/src/main/conf/local```
5. Установить локально postgresql 14 и настраиваем БД (пример для Linux)
  ```bash
  # устаналиваем pgostgres
  apt install postgresql-14

  # создаем пользователя
  createuser -dsP b2b-customers

  # создаем администратора
  createuser -dsP mdb_admin

  # создаем базу данных
  createdb -O b2b-customers b2b-customers

  # сохраняем пароль от БД тестинга (альтернативно его можно указать в самой команде pg_dump --password)
  export PGPASSWORD="[PGAAS_PASSWORD](https://yav.yandex-team.ru/secret/sec-01g3ztnbja6pje9wyyenv62a5m/explore/versions)"

  # создаем дамп БД [тестинга](https://yc.yandex-team.ru/folders/akugt7rrckrcb029but5/managed-postgresql/cluster/mdb97cptpatjminge898?section=overview)
  pg_dump --format=c --file=b2b-office-tst.backup --no-sync -d b2b-customers -h vla-8knb8vnd32g2n5d4.db.yandex.net -p 6432 -U b2b-customers

  # восстанавливаем дамп (для корректной работы должно быть 3 пользователя: postgres (по-умолчанию обычно создается), mdb_admin и b2b-customers)
  pg_restore -d b2b-customers -F c -U b2b-customers -W -h localhost b2b-office-tst.backup
  ```
6. В ```application/src/main/properties.d/local/local.properties``` сохраняем содержимое [local.properties](https://yav.yandex-team.ru/secret/sec-01g62wf6fp3v767hnd7k8rrvqc/explore/versions).
   Для отключения аутентификации выставляем в `local.propertes` `authentication.enabled=false`.

7. Запуск фронта https://a.yandex-team.ru/arcadia/market/jmf/webapp
 - Устанавливаем NodeJS 14 версии
 - Создаем файл `arcadia/market/jmf/webapp/.env` с содержимым:
   ```
   PROJECT_NAME=market-b2b-office
   CDN_URL=http://localhost:8080
   ```
8. Для запуска бека используем `Run application` из пункта #2, для запуска фронта скрипт `arcadia/market/jmf/bin/serve-local.sh`
