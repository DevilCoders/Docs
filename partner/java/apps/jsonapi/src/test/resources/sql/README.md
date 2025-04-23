Варианты запуска
-
1. С переменной окружения SQL_SOURCE_PATH<директория или файл где храняться тест (Должны быть ниже /sql)>.
Если есть переменная окружения SQL_SOURCE_PATH, то будут выполняться лиш тесты находящиеся ниже по дереву

Пример:
``SQL_SOURCE_PATH=/Users/leontevml/arc/arcadia/partner/java/apps/jsonapi/src/test/resources/sql/users ya make -tt -F=*SqlTest*``

2. SELF_UPDATE=1, перед проверкой ответов каждого теста будет обновлять тег файл с sql
