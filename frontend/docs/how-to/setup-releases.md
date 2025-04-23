# Подключение автоматизации релизов

Настраиваем автоматизацию [релизного процесса](../faq/release-workflow.md#Описание-релизного-процесса-сервисов-в-монорепозитории) сервиса.

## Терминология
* **<сервис>** - имя вашего сервиса в package.json после префикса `@yandex-int/`;

### ABC
Добавьте вашу команду разработчиков и тестировщиков в [ABC сервис frontend][abc-frontend]. Это нужно, чтобы у всех в команде была возможность запускать сборку frontend в CI.

### Права доступа к веткам и тегам
:warning: Подробно про права написано в [документации][branches-acl] arc.

#### Релизные ветки
В IDM запросите ответственному за сервис роль **Prefix admin** на префикс `releases/frontend/<сервис>/`. Роль **Prefix admin** позволяет управлять правами на все ветки в префиксе и выдавать права остальным. После того, как ответственный получил роль **Prefix admin** запросите разработчикам роли **Create** и **Fast-forward push** на префикс `releases/frontend/<сервис>/`.

#### Релизные теги
В IDM запросите ответственному за сервис роль **Prefix admin** на префикс `tags/releases/frontend/<сервис>/`. После того, как ответственный получил роль **Prefix admin** запросите разработчикам роль **Create** на префикс `tags/releases/frontend/<сервис>/`.

### Настройка `a.yaml`
1. Скопируйте шаблон конфигурационного файла [a.template.yaml] в `a.yaml` в папке сервиса.
1. Замените `<your-service-name>` в шаблоне на имя сервиса.
1. В `title`: __Стаб для новых проектов__ переименуйте, можно на название вашего сервиса;
1. В `ci.releases.release.title`: __Стаб для новых проектов__ переименуйте, можно на название вашего сервиса;
1. В `ci.flows.release-flow` заполните релизные префиксы и шаблон релизного тикета:
    1. В `path_in_arcadia` укажите путь до вашего сервиса в арке, путь указываем от корня Аркадии;
    1. В `release_branch_prefix` укажите префикс релизных веток;

> :warning: Важно: Обратите внимание, что релизные префиксы должны заканчиваться слэшом `/`!

Подробнее про настройки тасклета `common/frontend/release/create_release` читайте [документацию][create_release].

### Точка отсчёта версий
Для того, чтобы автоматика начала подхватывать релизы, необходимо вручную проставить первый релизный тег в формате `tags/releases/frontend/<сервис>/vX.Y.Z`.

```
arc push <коммит>:tags/releases/frontend/<сервис>/vX.Y.Z
```

[abc-frontend]: https://abc.yandex-team.ru/services/frontend/
[branches-acl]: https://docs.yandex-team.ru/devtools/src/arc/branches#acl
[a.template.yaml]: ../../services/stub/a.template.yaml
[create_release]: https://a.yandex-team.ru/arc/trunk/arcadia/ci/registry/common/frontend/release/create_release.md
