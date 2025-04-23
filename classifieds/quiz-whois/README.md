# quiz-whois

Вертикальные Создатели:
* [matreshka](https://staff.yandex-team.ru/matreshka)
* [agrigorev](https://staff.yandex-team.ru/agrigorev)
* [natix](https://staff.yandex-team.ru/natix)
* [timondl](https://staff.yandex-team.ru/timondl)
* [aandrosov](https://staff.yandex-team.ru/aandrosov)

Можно им писать вопросы и предложения.

## Как поднять у себя

**Disclaimer:** стоит понимать, что сервис создавался как pet-project в Вертикалях.
Многие штуку завязаны на Вертикальный деплой (shiva) и всю инфраструктуру вокруг.

Технологии: node.js, typescript, react, YDB

Проект собирается в docker-контейнер:
```sh
$ YENV=production make deps
$ YENV=production make build
$ docker build -f Dockerfile . 
```

Для запуска контейнера надо передавать в него следующие env:
* `_DEPLOY_G_TVM_ID=XXXXXX` - tvm_id приложения (для доступа к YDB и blackbox.yandex-team.ru). В базе YDB надо настроить доступы и заказать [гранты в паспорте](https://forms.yandex-team.ru/surveys/4901/). Пример [таска](https://st.yandex-team.ru/PASSPORTGRANTS-7856).
* `_DEPLOY_G_TVM_SECRET=XXXXXX` - tvm-секрет
* `_DEPLOY_METRICS_PORT=81` - порт prometheus
* `APP_ROOT=/opt/quiz-whois` - корневая директория проекта
* `AVATAR_SECRET_KEY=XXXXXX` и `AVATAR_SECRET_SALT=XXXXXX` - ключ и соль для шифрования (используются для шифрования данных загадки)
* `HEAD_UID=1120000000000305` - UID руководителя сервиса/БЮ. Логика такая: первым загадывается HEAD_UID, вторым непосредственный руководитель, дальше случайные коллеги.
* `NODE_ENV=production` - окружение приложения (в контейнере целесообразно всегда иметь `production`)
* `NODE_EXTRA_CA_CERTS=/usr/share/yandex-internal-root-ca/YandexInternalRootCA.crt` - путь до серта InternalCA, чтобы работали запросы в center-robot.yandex-team.ru
* `NODE_PORT=80` - порт, на котором поднимается node.js
* `STAFF_REQUEST_URL=ХХХХХХ` - урл с запросом в https://staff-api.yandex-team.ru, чтобы выкачать нужное подразделение на стафе
* `STAFF_OAUTH_TOKEN=XXXXXX` - OAuth-токен для доступа к staff
* `TVM_DESTINATION_BLACKBOX_YT=223` - tvm_id blackbox.yandex-team.ru
* `TVM_DESTINATION_YDB_ID=2002490` - tvm_id YDB
* `YDB_ENTRYPOINT=grpc://ydb-ru.yandex.net:2135` - адрес YDB
* `YDB_DB=/ru/verticals/production/autoru` - адрес YDB-базы
* `YDB_TABLE_PREFIX=/ru/verticals/production/autoru/frontend/quiz-whois` - префикс для таблиц. Внутри этой папки приложение создаст свои таблицы.

Пример `STAFF_REQUEST_URL` для Вертикалей:
```
https://staff-api.yandex-team.ru/v3/persons?_limit=5000&_query=(official.organization.id%3D%3D25%20or%20official.organization.id%3D%3D30%20or%20department_group.url%20%3D%3D%20%22yandex_edu_personel_rec_second_five_0598%22)%20and%20department_group.ancestors.url%20!%3D%20%22outstaff%22&_fields=uid,login,name.first.ru,name.last.ru,official.position.ru,personal.gender,location.office.city.name.ru,official.is_dismissed,department_group.name,telegram_accounts,chief.uid
```

В деве секреты выкачиваются из секретницы (`make .env.secrets`), конфиг находится в файле `secrets.config.json`

При старте приложения запускается `server/startupTasks.ts`, который создает таблицы в YDB и выкачивает нужные ветки стаффа.
Приложение само обновляет стафф раз в час.

## Разработка

На сервере: `make`. watch-режим для TS - `make tsc-watch`

Перед нодой надо поставить nginx в домене yandex-team.ru, который будет терминировать HTTPS и проксировать запросы в ноду. Пример конфига `configs/nginx.conf`.

## Полезности

Переливка из прода в тестинг:
* Загружаем ya tool https://wiki.yandex-team.ru/yatool/distrib/
* Копируем персональный ключ доступа в .ydb/token https://ydb.yandex-team.ru/docs/getting_started/ydb_cli
* mkdir my_backup_of_basic_example
* ya ydb -e ydb-ru.yandex.net:2135 -d /ru/verticals/production/autoru tools dump -p /ru/verticals/production/autoru/frontend/quiz-whois -o my_backup_of_basic_example/
* ya ydb -e ydb-ru-prestable.yandex.net:2135 -d /ru-prestable/verticals/testing/common tools restore -p /ru-prestable/verticals/testing/common/quiz-whois -i my_backup_of_basic_example/ 
