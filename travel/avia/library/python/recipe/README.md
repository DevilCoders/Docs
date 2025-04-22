Рецепт авиа
===========

Рецепт используется для настройки окружения при тестировании.
В рецепте авиа задействованы:
- рецепт поднимающий демон mysql (общий travel рецепт https://a.yandex-team.ru/arc/trunk/arcadia/travel/library/recipes/library/mysql.py)
- рецепт для наливки mysql схемы (общий travel рецепт https://a.yandex-team.ru/arc/trunk/arcadia/travel/library/recipes/library/mysql_schema.py)

После настройки в окружении доступны переменные окружения:
- AVIA_MYSQL_BIN - путь до исполняемых mysql утилит (mysql, mysqldump ...)
- AVIA_MYSQL_PORT - порт на котором поднят демон mysql
- AVIA_MYSQL_DATABASE - название сгенерированной тестовой базы
