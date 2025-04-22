# stat-bot

Телеграм боты для аналитической отчетности и алертов.

### Боты:
- `@RealtyMoneyBot`
- `@RabotaMoneyBot`
- `@AutoruStatBot`
- `@VertisMarketingStatBot`
- `@TeleponyStatBot`

### Структура проекта
```
.
├── Makefile
├── cmd
├── config
├── githooks
├── internal
│  ├── handler
│  │  ├── alert
│  │  ├── report
│  |  └── command
|  └── ...
├── pkg
└── vendor
```

* `Makefile` - основной сборщик для репозитория
* `cmd` - тут лежат пакеты c `main()`
* `config` - конфиги и переменные окружения
* `githooks` - git хуки, запускаемые перед коммитом / пушем / т.п.
* `internal` - внутренние пакеты проекта
* `internal/handler` - обработчик команд бота
* `internal/handler/alert` - алерты
* `internal/handler/report` - отчеты
* `internal/handler/command` - команды
* `pkg` - общие пакеты для всех сервисов, утилит и пр.
* `vendor` - go mod зависимости

Пакеты именуются через `kebab-case`, файлы именуются через `snake_case`. Бинарники тоже именуются через `kebab-case`.

> Подробнее про высокоуровневую структуру проектов на Go:
>   * https://medium.com/golang-learn/go-project-layout-e5213cdcfaa2
>   * https://github.com/golang-standards/project-layout

### Инициализация репозитория

Если вы впервые работаете с данным репозиторием то, после того как вы
склониуете его себе, запустите:

```sh
$ make init
```

Данная команда подготовит все необходимое для работы с репозиторием: установит
утилиты, зависимости, git hook'и и т.п.

### Именование рабочих веток
Используем соглашение: `<TICKET-NAME>/human-readable-description`. Коммиты в master не закрыты, но не поощряются, лучше создать Pull Request, в котором коллеги посмотрят изменения.
