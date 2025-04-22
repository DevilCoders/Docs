# Lavkach

Все пакеты в requirements.txt
Так же нужна переменная в env SECRET_KEY для запуска

### Локальный запуск

#### Без uwsgi и nginx
1. Установить зависимости
   ```
   pip install --index-url https://pypi.yandex-team.ru/simple/ -r requirements.txt
   ```
2. Запустить базу:
   ```
   make start_db
   ```
3. Выставить переменные окружения
   ```
   export SECRET_KEY=<ключ django>
   export AWS_ACCESS_KEY_ID=<id ключа amazon>  # если нужeн S3 
   export AWS_SECRET_ACCESS_KEY=<ключ amazon>  # если нужey S3
   export TEAM_OAUTH_CLIENT_ID=<id клиента>  # если нужен OAuth
   export TEAM_OAUTH_CLIENT_SECRET=<ключ клиента>  # если нужен OAuth
   export TG_BOT_TOKEN=<токен телеграм-бота>  # если нужен telegram
   ```
4. Запустить миграции
   ```
   python web/manage.py migrate
   ``` 
5. Запустить приложение
   ```
   python web/manage.py runserver 
   ```

#### Через uwsgi и nginx
##### Запустить
```
make start_back
```

##### Остановить
```
make stop_back
```

### Полезные ссылки
* [Postgres](https://yc.yandex-team.ru/folders/akuu6th37s0ntlrk0jme/managed-postgresql)
* [Dorblu stable](https://grafana.yandex-team.ru/d/46OxbiIMz/nanny_lavka_lavkach_stable?orgId=1&refresh=30s)
