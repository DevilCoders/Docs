# тест на запуск приложения web в сборе

Сервер запускается с типом окружения production, но с подменёнными db_config и network-config.
Не ожидается, что к базам можно законнектиться.

Дёргаются ручки alive и admin?action=version, проверяются что приложение хоть как-то запустилось
и ApplicationContext смог собраться.
