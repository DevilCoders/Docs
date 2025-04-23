Как обновить конфигурационные файлы Кликфита для Репорта:

* Поменять `market/tools/develop/dashboards/clickphite_config_gen/clickphite_config_gen.py`.
* Выполнить`./clickphite_config_gen.py --dump` и поревьюить изменения в подкаталоге `configs`.
* Опубликовать изменения: `PYTHONHTTPSVERIFY=0 HEALTH_AUTH_TOKEN=<token> clickphite_config_gen.py --publish`.

Токен брать тут: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=05940c6441d549c685b3e6bdc097cd55
Есть ключ `--config-name` который позволяет обновить только избранные конфиги.

Графики начнут строиться по новым конфигам через несколько минут.
