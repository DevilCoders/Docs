# Бэкенд для просмотра текущих релизов
Для dev окружения сначала создать базу (через psql например)

```sql
CREATE USER youruser;
CREATE DATABASE rviewer_test_db OWNER youruser;
ALTER USER youruser  WITH PASSWORD 'youruser_pass';
```

Переходим в созданную БД
```
\c rviewer_test_db
```

Создаем схему
```sql
CREATE SCHEMA rviewer AUTHORIZATION youruser;
```


В своём dev-окружении пароль нужно положить в переменные окружения имя БД, логин , пароль к БД и OAUTH токен с доступом в Nanny
```
export OAUTH_TOKEN=TOKEN # токен к няне
export YT_TOKEN=TOKEN  # токен с доступом к YT
export INFRA_TOKEN=TOKEN # токен к infra
export DB_NAME=rviewer_test_db
export DB_USER=youruser
export DB_PASS=youruser
```
Cобираем бинарник через `ya make`

### После этого создать базу 

```
./rviewer_exec --config config/config.yaml --db-init
```

### Скопировать сертификат: 
`wget "https://crls.yandex.net/allCAs.pem" -O config/allCAs.pem`


### Запуск приложения
Добавить в конфиг файл `development: true`, если отсутствует
 
```
./rviewer_exec --config config/config.yaml
```

Можно запускать дебаггером, если прописать PYTHONPATH=<ARCADIA_PATH>

### UI

[Склонировать frontend ](https://github.yandex-team.ru/Marty/Rviewer)

`npm install && npm run build`

`cp -r build/* $arcadia/search/mon/rviewer/static/`
