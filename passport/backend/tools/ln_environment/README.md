Утилита ln_environment
----------------

Создаёт лимлинки аналогично дебхелперу dh_environment. В отличие от дебхелпера, умеет больше окружений (например, rc), а также умеет фолбечиться (например, на конфиги для тестинга, если нет специальных конфигов для дева).

Если симлинк уже существует - он будет перезаписан.

Пример использования:
```
$ ./ln_environment /etc/nginx/conf-available/my_conf /etc/nginx/conf-enabled/my_conf
Created symlink /etc/nginx/conf-enabled/my_conf -> /etc/nginx/conf-available/my_conf.testing

$ ./ln_environment /etc/nginx/conf-available/my_conf2 /etc/nginx/conf-enabled/my_conf2
Failed to created symlink for /etc/nginx/conf-available/my_conf2: no config suitable for env_name=localhost, env_type=development
```
