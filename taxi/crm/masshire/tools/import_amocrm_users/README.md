# Загрузка пользователей amoCRM

Используется, чтобы выгружать маппинг из Яндексового логина рекрутера в идентификатор пользователя в amoCRM. Запускается ежедневно в Sandbox с помощью задачи `RUN_BINARY_RESOURCE`. Ресурс с бинарником можно найти по атрибуту `binary=import_amocrm_users`.

Поддерживает возможность ходить в прод/тестинг аккаунт в amoCRM и, соответственно, записывать данные в прод/тестинг БД модуля поиска.
