Девелопмент:
```
pip install --user -i https://pypi.yandex-team.ru/simple/ -r deps/python-dev.txt
```
также для разработки нужен docker и docker-compose.

На `uhura-dev.sas.yp-c.yandex.net`:
```
export COMPOSE_PROJECT_NAME=<username>_uhura
```

Собрать модель на `uhura-dev.sas.yp-c.yandex.net` (локально будет очень долго):
```
fab build_model
```

Собрать проект:
```
fab build_project
```

Запустить тесты:
```
fab test
```

Залить в registry тестовый образ:
```
fab build_project:env=testing,push=True
```

Попасть в контейнер:
```
docker-compose run app bash
```
или соответствующая fab-команда.


Работа с логами:

 * скопировать логи наших приложений из кулаудных логов к себе в кластер YT (откуда начинать копировать скрипт смотрит
   из табличек YT):
```
python cli/copy_dialog_logs.py --qloud-app uhura --qloud-env telegram-production --source-dir
'//home/logfeller/logs/qloud-runtime-log/1d' --destination '//home/intrasearch/uhura/dialog_history/telegram/production'
```
 * обработать логи произвольно, например:
   https://yql.yandex-team.ru/Operations/WZ8JulEZjVMkVcpSAbF4KTkK5K5hr3ocUwGF8TEEaDk=
   https://yql.yandex-team.ru/Operations/WZ_hN1EZjVMkVeeG88KMGp8PQCm1Acj01lUAgYUxOYw=

 * погрепать наши логи из кулаудных: https://yql.yandex-team.ru/Operations/WZ7MdB1icf0Z-FLtY4IvVumyta3fQJVozWNH_4_dEeY=


Для пулл реквестов из консоли (см. fabfile.py):
 * установить https://github.com/github/hub (на uhura-dev установлено)
 * получить токен для гитхаба https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/
 * прописать токен в env:
```
export GITHUB_TOKEN=<token>
```

Как проверить оповещения о ЧС в developmente:

 * на uhura-dev (на этот порт проковыряна дырка из КФ на виртуалку):
```
export UHURA_PORT=32768
```
 * fab run:"uhura createsuperuser" - если до этого суперюзер для админки не был создан
 * fab run:"uhura runserver 0.0.0.0:80"
 * зайти из браузера на http://uhura-dev.haze.yandex.net:32768/admin/ и залогиниться
 * прописать себя в Emergency notifiers и в Emergency testing lists
 * заполнить форму https://forms.yandex-team.ru/surveys/5684/
 * девелоперское оповещение должно придти, в телеграм (может и в ямб), в личную почту и на телефон
 
 ## Выкатка
 ```
   fab build_model
   fab release
   fab deploy:bot_type=telegram 
 ```
 в прод
 ```
   fab build_model
   fab release
   fab deploy:qloud_env=production
 ```
