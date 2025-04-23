## Описание
https://wiki.yandex-team.ru/intranet/femida/dev/

## Coding guidlines
https://wiki.yandex-team.ru/intranet/femida/dev/coding-guidelines/

## Локальная разработка
 Сейчас локальный запуск сервиса не работает, либо работает некорректно. Локально запускаем только тесты, для остального используем стенды.
 Пример стенда: https://deploy.yandex-team.ru/stages/tools_femida_stand
 - `make build-local` - для первого запуска
 - `make run-local` - для последующих запусков
 - Заходим в браузере на http://localhost:8000 (порт можно поменять через `FEMIDA_PORT`)

### Make-команды
- `make arc-build` – соберёт бинарь `femida-main`
- `make stand name=<name>` – выкатит приложение на стенд, если надо поднимет новый (команда для Qloud, в Деплое используйте `ya tool releaser stand -s <stand>`)
Стенды для отдельных PR у нас принято называть `pr-<id>`.
- `make delete-stand` – удалит стенд (команда для Qloud)

### Миграции
- `./manage.sh makemigrations <app>` – создание миграций

Чтобы применить миграции на стенде или тестинге:
- выкатываем туда новый код
- заходим на любой pod по ssh
- `femida showmigrations` – полный список миграций
- `femida migrate <app> <migration_id>` – применить миграцию

Чтобы применить миграцию в проде:
- `ya tool releaser deploy -c migrations:migrations -e tools_femida_production` – выкатить последнюю версию кода на отдельный DU `migrations`
- `femida migrate <app> <migration_id>` – применить миграцию
- `femida update_permissions` – Если надо обновить глобальные доступы
- выкатить код в основные DU

Все django management-команды выполняются через `femida ...`

### Новые настройки constance
Если в коде появляются новые настройки constance, которые будут вызываться в slave-режиме БД,
их надо явно вызвать предварительно на DU migrations, чтобы в master-режиме в БД сохранилось дефолтное значение настройки.
- `ya tool releaser deploy -c migrations:migrations -e tools_femida_production` – катимся на `migrations`
- `femida constance get <CONFIG_NAME>` – получаем настройку, триггерим запись дефолта в БД

## Сборка и деплой
 Делаем с ноута, на котором стоит releaser.
 - `ya tool releaser release` - сборка нового релиза и выкатка в тестинг
 - `ya tool releaser stand -s <stand>` - выкатить стенд (без сборки)
 - `ya tool releaser deploy -e tools_femida_production` - выкатить текущую версию в прод
 - `ya tool releaser deploy -e tools_femida_production -c migrations:migrations` - выкатить в отдельный deploy-unit

### Создание стенда
https://wiki.yandex-team.ru/team-fennec/femida/backend/stands/

### Быстрая выкатка на стенд
Иногда есть необходимость быстро выкатить и проверить изменения на 1-2 хостах стенда.
В таких случаях нет смысла собирать новый docker-образ, а потом ждать полноценной раскатки релиза через deploy.
Можно сделать примерно следующее:
1. Собираем бинарь Фемиды под linux и загружаем его на стенд
```
ya make --target-platform=linux -o build-linux \
  && scp build-linux/intranet/femida/src/wsgi/femida.wsgi root@${FEMIDA_STAND}:femida-main-linux
```
2. Заходим на хост по ssh
3. Убиваем процесс и подменяем бинарь. Ждём пока приложение снова запустится
```
pkill -9 femida-main && mv femida-main-linux femida-main
```

Для упрощения заливки на DU `backend` своего стенда, можно где-нибудь в .bashrc/.zshrc задать переменную окружения
```
export FEMIDA_STAND="<backend-host>"
```
Дальше просто использовать готовый шорткат для заливки бинаря
```
make fast-stand
```


## Запуск тестов
 - `ya make -A` - запустить все тесты
 - `ya make -AP` - запустить все тесты и показать результат для успешных
 - `ya make -A -F unit.core.db.test_expressions.py` - запустить конкретный модуль
 - `ya make -A -F "unit.core.db.test_expressions.py::test_jsonf*"` - запустить конкретный тест

## Работа с письмами (возможно, не работает после переезда в Аркадию)
 - `docker-compose build mail`
 - `docker-compose up mail`
 - `localhost:8888` в браузере

## Code review
 - https://github.yandex-team.ru/devexp/devexp#Как-подключить-к-себе

## Дополнительно
- [Конфиги nginx для yandex.ru/hire](../femida-nginx-hire/)
