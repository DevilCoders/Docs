# tun

Сервер для поднятия ssh-туннелей с аутентификацией через staff-api.

Основан на [tunneler@1.1.3](https://github.yandex-team.ru/toolbox/tunneler). Основные отличия:
- Отсутствует http-прокси – эту роль теперь выполняет балансер.
- TLS терминация на балансере – больше никаких переключений протоколов.
- Аутентификация через staff-api с ретраями.
- Структурированное логирование.

## HTTP API v2

Где API v1? От него пришлось отказаться для возможности роутинга в приложениях, где используется tunneler (например, в переходный период). HTTP API tun и tunneler несовместимы.

### `GET /api/v2/instances`

Возвращает список хостов, на которые можно подключаться:

```json
[{
    "host": "myt1-043636b9c887.qloud-c.yandex.net",
    "port": 2022
}]
```

## Развертывание

Проект размещается в Deploy (ферма инстансов в YP):
- [tun](https://deploy.yandex-team.ru/stage/tun)
- [tunneler-ws](https://deploy.yandex-team.ru/stage/tunneler-ws)

Образ – `registry.yandex.net/search-interfaces/tun`.

Необходимые переменные окружения:
```sh
TUN_API_PORT=8000
TUN_SSH_PORT=2022
TUN_SSH_HOST_KEY=/hostkey
STAFF_TOKEN=****
```

В `/hostkey` должен быть смонтирован секрет с ключом хоста (секрет `tunneler-ci-priv-key` для совместимости с tunneler).

Для доступа к `staff-api` используется [токен](https://yav.yandex-team.ru/secret/sec-01d6fw5tgqy91z97j3ry6vygmd/explore/version/ver-01d6fw5thzerddsehn9gw1ae7k) робота `robot-serp-bot`.

## Дашборды
- [Панели балансера](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/tun/monitoring/common)
- [Инстансы tun](https://deploy.yandex-team.ru/project/tun/monitoring)
- [Инстансы tunneler-ws](https://deploy.yandex-team.ru/project/tunneler-ws/monitoring)

## Использование локально

https://doc.yandex-team.ru/si-infra/tunneler/troubleshooting.html

## Использование в CI

https://doc.yandex-team.ru/si-infra/tunneler/troubleshooting.html

## Разработка

```sh
npm ci
cp .env.example .env
```

В `./hostkey` нужно положить приватный ключ хоста.

Запуск сервера:

```sh
npm run dev
```

Создание тестового туннеля (слушает 8081, заворачивает на 8080):

```sh
node client.js
```

## Публикация новой версии

Обновить версию в `package.json`, выполнить `make docker-publish`.
