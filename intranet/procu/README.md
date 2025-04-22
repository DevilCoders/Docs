# Backend Закупок

## Перед разработкой

1. Настроить прекоммитные хуки (с помощью них запускается [Black](https://github.com/ambv/black))
   ```
   pip install pre-commit
   pre-commit install
   ```

2. Настроить виртуальные хосты. Нужно добавить в `/etc/hosts`:
   ```
   127.0.0.1 procu.int
   127.0.0.1 procu.ext
   ```

   Соответственно, на `http://procu.int:80` будет доступен внутренний API (с аутентификацией через blackbox), на `http://procu.ext:80` — внешний (с аутентификацией по логину и паролю).

   Запросы на другие хосты в dev-окружении будут возвращать ошибку.

3. Создать файл `etc/datasources/datasources-local.py`, если требуется запускать ручки, зависящие от секретов. Его содержимое есть на соответствующей [вики-странице](https://wiki.yandex-team.ru/Intranet/procu/secrets/). Git игнорирует этот файл.

4. Сделать миграцию данных `docker-compose run api procu migrate`

5. Создать в базе все необходимые пермишшены `docker-compose run api procu permissions`

6. Завести себе пользователя и выдать ему админские права (через `procu createsuperuser` или отдельно выдать права через `user.set_roles('admin')`)

## Во время разработки
Для авторизации при локальной разработке есть отдельный мок блэкбокса, запускаемый через docker-compose.
Чтобы работала авторизация нужно поставить для домена procu.int куку `Session_id` со значением `|login:<your login>|`.

## Python зависимости

Зависимости хранятся в файлах `etc/deps/*.in`. Именно там их нужно редактировать и добавлять.

Одноимённые `.txt` файлы генерируются утилитой [pip-compile](https://github.com/jazzband/pip-tools):

```
pip-compile --generate-hashes -o etc/deps/python.txt etc/deps/python.in
```

Из них собирается образ. Они содержат транзитивные зависимости с фиксированными версиями. Править их руками не нужно.
