[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=yandex360/frontend/services/api360&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/services/api360)
[![oko health](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=yandex360/frontend/services/api360&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/services/api360)

# Api360

REST/gRPC сервис для административных задач сервиса 360.

Страница на wiki https://wiki.yandex-team.ru/yandex360/admin/api/

Тестовый сервер живёт по адресу https://api360-testing.mail.yandex.net/

## Быстрый старт
Для запуска нужен docker и docker-compose.

```bash
npm ci
make start
```
Эта команда запускает `docker-compose` c приложением и `envoy`.

Проверить работу REST можно из консоли:
```bash
# ping
curl http://localhost:8080/ping
# {}

# say
curl http://localhost:8080/say?name=Vasya
# {
#  "message": "Hello, Vasya!"
# }

# whoami
curl http://localhost:8080/whoami -H "Authorization: OAuth $OAUTH_TOKEN"
#{
# "login": "lynntest",
# "scopes":["directory:read_users","directory:read_departments"]
#}
```

OAuth-токен можно взять тут https://oauth-test.yandex.ru/authorize?response_type=token&client_id=5527322964384eb5ac3ffa9ae975ffd3
(авторизация тестовым паспортом).

Тестовые приложения где можно завести организацию:
- https://connect-test.ws.yandex.ru/portal/admin/
- https://admin.dst.yandex.ru/

## Работа с отделами
```bash
# получить информацию
curl http://localhost:8080/directory/v1/org/103378/departments/1 -H "Authorization: OAuth $OAUTH_TOKEN"
# {
#  "id": 1,
#  "name": "Все сотрудники",
#  "parentId": 0
# }

# изменить информацию
curl http://localhost:8080/directory/v1/org/103378/departments/6 -H "Authorization: OAuth $OAUTH_TOKEN" -X PATCH -d '{"name":"Новое имя"}'
# {
#  "id": 6,
#  "name": "Новое имя",
#  ...
# }
```

Для работы по gRPC есть пример приложения `client.ts`. Запустить можно командой
```bash
make run-client
```
Приложение ожидает OAuth-токен в переменной окружения `OAUTH_TOKEN`.

## HOWTO

* [HOWTO для разработки](./doc/README.md)
