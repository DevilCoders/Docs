Миграция java-sec ролей через ручку java-sec-http-proxy

Как составить схему:
1. `auth.csv` - здесь перечислены роли и чекеры, которые эти роли будут проверять. Про то как это работает можно почитать [тут](<https://wiki.yandex-team.ru/MBI/NewDesign/javasec/>).
2. `op.csv` - операции и операции к ним
3. `permissions.csv` - пермиссии, здесь мы говорим, что такая роль, может выполнять такую операцию. Здесь еще есть параметр, который можно передать в чекер(такая операции доступна для такой роли, только при таком то условии)
4. `auth_links.csv` - линки ролей. Здесь мы говорим, что проверяя какую-то роль, нужно или можно(and и or соответсвенно) проверить еще какую-то.



Как добавить csv схему в мигратор:
1. Создать схему, папка должна быть названа как ваш java-sec домен и лежать в java package
```ru/yandex/market/security/migration/csv``` [пример](<https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/mbi/mbi-java-sec-csv/src/resources/ru/yandex/market/security/migration/csv/mbi-partner>).
Ваши csv необходимо оформить отдельной java библиотекой и сложить куда хотите в аркадии
[пример](<https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/mbi/mbi-java-sec-csv/ya.make?rev=6980520#L4>).
2. Далее необходимо добавить бибилиотеку с вашими csv в мигратор, чтобы он подхватывал изменения и собирался с вашими новыми csv [сюда](<https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/java-sec/java-sec-migrator/ya.make?rev=7159193#L14>).
3. Добавить ваш домен в [этот массив](<https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/java-sec/java-sec-migrator/src/main/java/ru/yandex/market/security/migration/Migrator.java?rev=7159193#L29>). Чтобы запускались тесты, в которых проверяется, что ваша схемка валидная.
4. В ваш пайплайн добавить кубик, который будет собирать мигратор
```
Sandbox Market Ya Package Job Config:
pkg: market/mbi/java-sec/java-sec-migrator/package.json
resource type: MARKET_JAVA_SEC_MIGRATOR_APP
```
5. И кубик, который будет запускать его `JavaSecMigrationJob`
конфиг:
Environment: development/testing/production
Domain: название вашего домена: например `mbi-partner`
Task type: MARKET_JAVA_SEC_MIGRATION

пример можно найти в [пайплайне](<https://tsum.yandex-team.ru/pipe/projects/mbi/pipelines/mbi-arcadia-cd-pipeline/>)

