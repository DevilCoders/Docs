# Go common

Единое место с общими подходами, правилами, утвержденными и самостоятельными библиотеками для разработки приложения на go.

# How to use

*Например логгер*

1. В `go.mod` добавить строчку вида
```
replace (
    github.com/YandexClassifieds/go-common/log => ../go-common/log
)
```
2.  `go get github.com/YandexClassifieds/go-common/log`
3. `go mod vendor`

## Best library

Список библиотек для реализации различных потребностей.
Библиотеки могут как внутренние (находятся в данном репозитории), так и внешние рекомендуемые.

|  | Library | Example |
|---|---|---|
|  Configuration | [conf](conf)  |   |
|  Logging | [log](log) |   |
|  Yandex Blackbox | [blackbox](blackbox)  |   |
|  Yandex TVM | [tvm](tvm)  |   |
|  Retry | [retry](retry)  | [example](go-common/retry/example_test.go)  |
|  CLI | https://github.com/spf13/cobra  |  |
|  DI | Через конструкторы в main  |  |

## Best practices

Общепринятые практики

1. [Effective go](https://go.dev/doc/effective_go)
2. [Project structure](https://github.com/golang-standards/project-layout)
3. [Go Code Review Comments](https://github.com/golang/go/wiki/CodeReviewComments)
4. [Uber style guide](https://github.com/uber-go/guide/blob/master/style.md)


### Базовая архитектура сервиса
```
cmd
  my_service                // Микросервис
      api
        public
          handler.go        // Получает через DI user.Service
        private
          handler.go        // Получает через DI user.Service
      user
        user.go             // Как модель в БД, а также доменный объект для работы
        storage.go          // Приватный
        service.go          // Публичный API
      main.go               // Инициализация и DI (через конструкторы)
      ...                   // Здесь могут быть утилитарные шутки (makefile, dockerfile and etc)
pkg                         // Не привязанные к микросервисам компоненты
  staff                     // Внутренняя (внутри репозитория) библиотека
    internal                // Область видимости внутри директории
      client.go             // Приватный
      client_test.go
    service.go              // Публичный API
```

### Новый сервис

 1. Создать директорию в Аркадии https://a.yandex-team.ru/arcadia/classifieds/infra/my_project
 2. Создать файл go.mod
 3. Добавить необходимые библиотеки из go-common
 4. Добавить a.yaml

## Best example

Здесь будут небольшие сервисы/библиотеки для подражания, на данный момент таких не обнаружено
