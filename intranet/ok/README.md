# ok

### Сборка
Окружение https://deploy.yandex-team.ru/projects/ok

Сборка и выкатка в тестинг: ```ya tool releaser release```

Выкатка в прод: ```ya tool releaser deploy -e tools_ok_production -dd```

### Разработка
Проект написан на ```python 3```

Если вы только начинаете разрабатывать, нужно всё приготовить.
Для этого нужно выполнить:
```
make dev-install
```
Команда соберёт нужные докер-образы, настроит БД и создаст супер-пользователя с вашим логином.

Если у вас нет доступа, то можно выполнить:
```bash
docker pull registry.yandex.net/tools/ok:<latest-version>
docker build . --cache-from registry.yandex.net/tools/ok:<latest-version>
make dev-install
```

В папке `settings` нужно создать файл `020-security.conf.local` с содержимым:
```
OK_ROBOT_TOKEN = "<свой oauth-токен какой-нибудь>"
```

Теперь можно запустить бэкенд:
```
make dev-run
```

Бэкенд будет доступен на порту 8000.
Сменить порт на другой можно через переменную окружения `OK_PORT`


### Тесты
Тесты запускаются при каждом PR через trendbox.

Чтобы прогнать тесты локально, нужно выполнить:
```
make test
```


### Миграции
Создание миграций
```
docker-compose run server ok makemigrations
docker-compose run server ok makemigrations <app_name>
```

Чтобы применить миграцию в проде:
- `ya tool releaser deploy -c console:console -e tools_ok_production -dd` – выкатить последнюю версию кода на отдельный DU `console`
- `ok migrate <app> <migration_id>` – применить миграцию
- выкатить код в основные DU


### Новые настройки constance
Если в коде появляются новые настройки constance, которые будут вызываться в slave-режиме БД,
их надо явно вызвать предварительно на DU console, чтобы в master-режиме в БД сохранилось дефолтное значение настройки.
- `ya tool releaser deploy -c console:console -e tools_ok_production -dd` – катимся на `console`
- `ok constance get <CONFIG_NAME>` – получаем настройку, триггерим запись дефолта в БД


### Обновление файла с переводами
При добавлении нового текста, который должен быть переведен пользователю, нужно добавить новые строки для перевода
в файл locale/ru/LC_MESSAGES/django.po, а затем прописать в него перевод новых строк ручками.
Добавление строк по доке django происходит через django-admin.py makemessages, в этом проекте настроена команда
```
make makemessages
```
После написание переводов руками, файл со строками нужно скомпилить аналогом django-admin.py compilemessages
```
make compilemessages
```


### Стенды
Создать стенд (если его ещё нет):
```
make stand
```
Создаст стенд в deploy (скопирует с `tools_ok_stand_base`, по-умолчанию) и настроит апстримы с тестового
бэкового балансера на него. Название stage со стендом по-умолчанию: `tools_ok_stand_<username>`.
Доступен будет на хосте `<username>.ok.test.yandex-team.ru`.

Выкатить код на существующий стенд:
```
ya tool releaser stand -s <полное название стейджа, куда нужно выкатить>
```
