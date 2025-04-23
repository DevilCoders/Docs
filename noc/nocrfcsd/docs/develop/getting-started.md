# Начало работы

## Настройка окружения

Нужно [установить Go](https://go.dev/doc/install), IDE/редактор и ознакомиться с
[Правилами разработки в Аркадии на Go](https://docs.yandex-team.ru/arcadia-golang/).

Желательно установить [golangci-lint](https://github.com/golangci/golangci-lint) версии, указанной в
[.golangci.yml](https://a.yandex-team.ru/arc_vcs/noc/nocrfcsd/.golangci.yml#L1).
Это мета-линтер, который содержит больше линтеров, чем стандартный аркадийный
[yolint](https://a.yandex-team.ru/arc_vcs/library/go/yolint), и поэтому предъявляет более строгие требования к коду.
К сожалению, пока не реализован запуск `golangci-lint` в CI.

Для сборки docker-образов и деплоя на тестинг понадобится [установить docker](https://docs.docker.com/engine/install/).

Желательно также поднять локально postgres с пустой базой `rfcs`. Например, через docker-compose:

```yaml
version: '3'

networks:
  postgres:

services:
  pg:
    restart: unless-stopped
    image: postgres:12-alpine
    # ускоряем работу postgres через монтирование data-директории в оперативную память
    tmpfs:
      - /var/lib/postgresql/data
    # включаем логирование всех запросов и ускоряем работу postgres, отключая fsync
    command:
      - -c
      - log_statement=all
      - -c
      - fsync=off
    ports:
      - 127.0.0.1:5432:5432
    environment:
      - POSTGRES_DB=rfcs
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres
    logging:
      options:
        max-size: "200k"
        max-file: "1000"
```

## Перед коммитом

Чтобы не тратить время на долгое ожидание нескольких запусков аркадийного CI, можно локально выполнить в директории
проекта все проверки:

```bash
golangci-lint run --fix
ya tool yo fix .
ya tool yoimports -w .
ya make -r -DGO_VET=yolint_next -tt --test-type=govet
ya make -tt .
```

Описание:

- `golangci-lint run --fix` - запускает мета-линтер `golangci-lint`, опция `--fix` заставляет мета-линтер автоматически
  исправлять проблемы, если это возможно
- `ya tool yo fix .` - запуск утилиты [yo](https://a.yandex-team.ru/arc/trunk/arcadia/library/go/yo), которая
  автоматически генерирует нужные файлы `ya.make`
- `ya tool yoimports -w .` - запуск утилиты
  [yoimports](https://a.yandex-team.ru/arc/trunk/arcadia/library/go/yoimports), которая исправляет Go-шные импорты
  согласно стилю, принятому в Аркадии
- `ya make -r -DGO_VET=yolint_next -tt --test-type=govet` - запускает Аркадийный мета-линтер
  [yolint](https://a.yandex-team.ru/arc_vcs/library/go/yolint)
- `ya make -tt .` - запускает тесты

Все команды (кроме первой) должны завершаться успешно. Если одна из них локально падает, то упадёт и аркадийный CI.

## Деплой на тестинг

Можно задеплоить на тестинг собранный вручную docker-образ. Для начала нужно убедиться, что есть доступ на запись
в docker registry в префикс `nocdev/`. Если его нет, то доступ можно получить по инструкции
[Docker distribuiton (ex. Docker registry) - Управление ролями](https://wiki.yandex-team.ru/docker-registry/#upravlenieroljami).
Образы nocrfcsd выкладываются в префикс `/nocdev`, поэтому при запросе роли в качестве сервиса нужно указать:
`Docker registry -> Префиксы -> nocdev/ -> contributor`.

Затем нужно авторизоваться в registry по инструкции
[Docker distribuiton (ex. Docker registry) - Авторизация](https://wiki.yandex-team.ru/docker-registry/#authorization).

Теперь можно переходить к сборке docker-образа:

```bash
ya package package.json --docker
```

Если сборка прошла успешно, то вывод закончится строками вида:

```
2022-01-21 03:52:47,823 Successfully built b540f012f7e2
2022-01-21 03:52:47,835 Successfully tagged registry.yandex.net/nocrfcsd:svn.9055110
Duration of package creation: 6.97s
```

В этом выводе виден тег свежесобранного docker-образа. Теперь нам нужно перетегировать этот образ:

- добавляем `/nocdev` в начале path: `registry.yandex.net/nocrfcsd:svn.9055110` `->`
  `registry.yandex.net`**`/nocdev`**`/nocrfcsd:svn.9055110`, чтобы образ попал в нужный префикс docker registry
- добавляем `-test` в конце тега: `registry.yandex.net/nocdev/nocrfcsd:svn.9055110` `->`
  `registry.yandex.net/nocdev/nocrfcsd:svn.9055110`**`-test`**, чтобы явно указать, что это тестовый docker-образ

Команда перетегирования:

```bash
docker tag registry.yandex.net/nocrfcsd:svn.9053109 registry.yandex.net/nocdev/nocrfcsd:svn.9053109-test
```

Далее можно залить перетегированный docker-образ в docker registry:

```
docker push registry.yandex.net/nocdev/nocrfcsd:svn.9053109-test
```

Переходим в
[Box settings / Resources](https://deploy.yandex-team.ru/stages/nocrfcsd-testing-stage/config/du-daemon/box-nocrfcs-daemon#resources)
нашего тестового стейджа в Yandex Deploy и редактируем тег образа:

![alt text](_assets/edit-docker-image-tag.png "Редактирование тега docker-образа" =952x598)

После этого сохраняем конфиг стейджа и ждём завершения деплоя.

## Деплой на продакшн

Для деплоя на продакшн:

- переходим на
  [страницу релизов](https://a.yandex-team.ru/projects/nocdev/ci/releases/timeline?dir=noc%2Fnocrfcsd&id=nocrfcsd)
- в правом верхнем углу нужного коммита выбираем `Release` и ждём завершения релиза

В ходе релиза CI сам соберёт docker-образ, зальёт его на docker registry и выкатит docker-образ на
[production stage](https://deploy.yandex-team.ru/stages/nocrfcsd-production-stage/).

## Быстрое выполнение тестов

Можно ускорить выполнение тестов, запустив их напрямую через `go` (без `ya make`). Нужно:

- иметь поднятый локально postgres с пустой базой `rfcs`, доступный по URL
  `postgres://postgres:postgres@localhost/rfcs` (либо же установить переменную окружения `POSTGRES_URI` с нужным
  connection string для соединения с базой)

Команда для запуска тестов:

```bash
go test ./...
```

Можно запустить отдельный тест, для тестов с testify suite:

```bash
go test $PACKAGE -run $SUITE_FUNCTION -testify.m $SUITE_METHOD_REGEX
```

Например:

```bash
go test a.yandex-team.ru/noc/nocrfcsd/internal/workflow -run TestFunctionalSuite -testify.m '^TestCreateRFC$'
```

## Snapshot-тестирование

Функциональное тестирование сделано с помощью YAML snapshot-ов
([википедия](https://en.wikipedia.org/wiki/Software_testing#Output_comparison_testing)) и с помощью декларативных
YAML-фикстур аналогичного формата. Например, чтобы перед тестом наполнить базу руками создаётся YAML-файл в
поддиректории `.input`, и заполняется данными через вызов вида:

```go
snapshot.Load(suite.T(), dbsnapshot.New(suite.tx))
```

Затем выполняется тестовый код и состояние базы сранивается со снимком ожидаемого состояния через вызов вида:

```go
snapshot.Snapshot(suite.T(), dbsnapshot.New(suite.tx))
```

Этот вызов выполняет сравнение полученного после теста актуального снимка с ожидаемым снимком, находящимся в
YAML-файле в поддиректории `.snapshots`. Если снимки не совпадают, то тест сфейлится и отобразится diff между
снимками.

При написании нового теста можно не создавать ожидаемый снапшот в `.snapshots`, а можно просто запустить
тест один раз: снапшот будет сгенерирован автоматически, и тест упадёт с ошибкой, указывающей на факт генерации
нового snapshot-файла.

При необходимости массово обновить все снапшоты можно облегчить себе работу, запустив тесты с переданной
переменной окружения `UPDATE_SNAPSHOTS` (не важно, какое именно значение передавать в эту переменную):

```bash
env UPDATE_SNAPSHOTS=1 go test ./...
```

или в случае `ya make`:

```bash
env UPDATE_SNAPSHOTS=1 ya make -tt .
```

Можно также обновить снапшот для одиночного теста:

```bash
env UPDATE_SNAPSHOTS=1 go test a.yandex-team.ru/noc/nocrfcsd/internal/workflow -run TestFunctionalSuite -testify.m '^TestCreateRFC$'
```

## Подсчёт покрытия тестами

```bash
go test -coverpkg=./... -coverprofile=cover.out ./...
go tool cover -html=cover.out
```
