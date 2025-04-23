## NewCI

[Наш проект в CI](https://a.yandex-team.ru/projects/portalvteam/ci?autoSelect=true)

### Configuration

CI для описания flow использует единый конфигурационный файл a.yaml,
который хранится вместе с кодом проекта.

Подробнее о содержимом файла:

-   [Быстрый старт](https://docs.yandex-team.ru/ci/quick-start-guide)
-   [Основы a.yaml](https://docs.yandex-team.ru/ci/basics)

### Runtime

Все задачи выполняются в сервисе [sandbox](https://sandbox.yandex-team.ru/).

Все что требуется знать о sandbox описано во [введении документации sandbox](https://docs.yandex-team.ru/sandbox/).

CI сам создает задачи в sandbox, на основании описания `job` в конфигурации CI.
Если `job` запустился в sandbox, то в задаче в UI CI есть ссылка на задачу в sandbox (лого sandbox в левом нижнем углу):

![img.png](img/sandbox-link.png)

Основное что может потребоваться внутри самого sandbox:

-   Просмотр логов исполнения - вкладка resources, иконка глаза в столбце Links.
    CI позволяет сократить этот путь и сделать прямую ссылку на логи самой задачи внутри кубика (второе с лева лого sandbox) с помощью флага `stdout_ci_badge`
-   Поиск задач можно осуществить на странице поиска, задав соответствующие фильтры, [пример](https://sandbox.yandex-team.ru/tasks?owner=TRAVEL-FRONT&tags=JOB-ID%3ARUN-E2E-FALLEN).
-   Просмотр доступной [вычислительной квоты](https://docs.yandex-team.ru/sandbox/quota) на [странице группы в sandbox](https://sandbox.yandex-team.ru/admin/groups/TRAVEL-FRONT/general)

Нашим задачам требуется предварительная настройка среды исполнения: установленная nodejs, npm, docker.
В CI и sandbox поддержана контейнеризация [LXC](https://linuxcontainers.org/lxc/introduction/):
Мы создали предварительно настроенный LXC-контейнер в sandbox [2961586335](https://sandbox.yandex-team.ru/resource/2961586335/view),
через [задачу](https://sandbox.yandex-team.ru/task/1270268832/view) в том же sandbox.
Ссылка на LXC-контейнер указана у нас в требованиях в конфигурации.

### Flows

Основная вещь, которой оперирует CI - это `flow`. Внутри `flow` можно исполнять несколько задач последовательно и параллельно,
запускать задачи в зависимости от выполнения определенных условий,
определять зависимости между задачами, требовать ручного подтверждения запуска задач и так далее.
Полный набор задач и связей между ними составляет граф исполнения.
Граф является ациклическим и направленным слева направо.
Задачи располагаются в узлах графа, а его ребра - это связи между задачами.
Для наглядности граф исполнения отображается прямо в пользовательском интерфейсе CI на соответствующей странице `flow`.

[Подробнее о возможностях flow](https://docs.yandex-team.ru/ci/flow)

### Actions and triggers

Для того чтобы `flow` попал в [пользовательский интерфейс CI](https://a.yandex-team.ru/projects/portalvteam/ci?autoSelect=true),
он должен быть объявлен в конфигурации в разделе `actions`.
Также для `actions` можно настроить автоматический запуск по триггерам.
Условия запуска триггеров можно дополнять используя [фильтры](https://docs.yandex-team.ru/ci/actions#filter).

[Подробнее о actions and triggers](https://docs.yandex-team.ru/ci/actions)

### Releases

Релиз - это особенный тип `flow`

-   [Внутренняя система нумерации (версий)](https://docs.yandex-team.ru/ci/release#versioning)
-   [Стадии](https://docs.yandex-team.ru/ci/release#stage)
-   [Создание релизных веток](https://docs.yandex-team.ru/ci/release#branches)
-   [Автоматический запуск по времени](https://docs.yandex-team.ru/ci/release#auto)

[Подробнее о релизах](https://docs.yandex-team.ru/ci/release)

### Versioning

[О версиях при релизах Docker и публикации npm пакетов.](versioning.md)

### Jobs

`job` - одна задача с входом и выходом внутри `flow`.

В поле task указывается путь до задачи из [реестра задач](https://a.yandex-team.ru/arc_vcs/ci/registry).

#### common/misc/run_command

Самый популярный тип задач, который мы сейчас используем - это

```
task: common/misc/run_command
```

Эта задача позволяет запускать произвольные bash скрипты в sandbox.
Для повторного использования bash скрипты мы выносим в папку ci общего родителя.

Через этот тип задач мы сейчас закрываем почти все свои потребности:

-   Запуск npm скриптов: проверки PR, автоматизированные действия (frigga)
-   Сборка и публикация npm пакетов
-   Сборка и публикация docker образов

Подробнее в [документации run_command](https://a.yandex-team.ru/arc_vcs/ci/registry/common/misc#common/misc/run_command).

#### common/tracker/create_issue

Готовая задача для создания релизных тикетов

[Документация](https://a.yandex-team.ru/arc_vcs/ci/registry/common/tracker#common/tracker/create_issue)

#### common/tracker/transit_issue

Готовая задача для смены статусов и комментирования релизных тикетов.

[Документация](https://a.yandex-team.ru/arc_vcs/ci/registry/common/tracker#common/tracker/transit_issue)

#### common/deploy/create_release

Выкатка релиза в Y.Deploy. Для нас - это просто обновления ссылки на Docker образ.

[Документация](https://a.yandex-team.ru/arc_vcs/ci/registry/common/deploy#sborka-i-vykladka-novogo-staticheskogo-resursa)

### Tricks and tips

-   Смотрите текущие реализации у нас в репозитории.
-   Используйте поиск по конфигурациям в аркадии. [Пример](https://a.yandex-team.ru/search?search=create_release,a.yaml,i,arcadia,,200&repo=arc_vcs)
-   Используйте YAML anchors для повторного использования частей конфига. О YAML anchors [в документации GitLab CI](https://docs.gitlab.com/ee/ci/yaml/yaml_optimization.html#anchorshttps://docs.gitlab.com/ee/ci/yaml/yaml_optimization.html#anchors)

### References

-   [Наш проект в CI](https://a.yandex-team.ru/projects/portalvteam/ci?autoSelect=true)
-   [Документация CI](https://docs.yandex-team.ru/ci/)
-   [Документация sandbox](https://sandbox.yandex-team.ru/)
-   [Страница группы в sandbox](https://sandbox.yandex-team.ru/admin/groups/TRAVEL-FRONT/general)
