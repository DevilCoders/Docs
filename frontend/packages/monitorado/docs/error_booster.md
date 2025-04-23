# Секция error_booster

- [Секция projects](#секция-projects)
- [Секция alertsets](#секция-alertsets)
    - [Алиасы для сигналов](#алиасы-для-сигналов)

Пример:
```yaml
error_booster:
  projects:
    # Имя проекта
    maps_project: default

  alertsets:
    default:
      settings:
        notifications: [chat, team]  # Кому отправлять уведомления
        runtime: nodejs  # Задаем runtime для всех алертов (если нужен не browserjs)
      alerts:
        # project=maps_project, type=script, platform=desktop
        script_error_desktop:
          signal: '%errors'
          crit: 3
          runtime: nodejs  # Можем переопределить runtime для алерта
          vars:  # Значения, которые подставятся в сигнал
            type: script
            platform: desktop
```

## Секция projects

Определяет соответствие `проект` -> `набор алертов`.

Например, для проекта https://error.yandex-team.ru/projects/ether/projectDashboard нужно указать `ether`.

## Секция alertsets

Базовый формат описан [тут](./common.md#Секция-alertsets).

Чтобы в Juggler-проверке алерта была правильная ссылка на графики в Error Booster, необходимо задать `runtime`. Это можно сделать либо через `settings.runtime` у алертсета
(тогда это применится ко всем его алертам, даже при наследовании), либо через `runtime` алерта. Значение по умолчанию - `browserjs`.

В сигналах можно использовать следующие плейсхолдеры, позволяющие переиспользовать сигнал для разных алертов:

* `{project}`
* `{type}`
* `{platform}`
* `{block}`
* `{source}`
* `{source_method}`
* `{environment}`
* `{service}`

Если в сигнале указан плейсхолдер, в поле `vars` алерта нужно указать значение, которые подставится вместо него.
Исключение - `{project}`, который автоматически заменяется на текущий проект.

Вместо `type` предпочтительно передавать `source`.

Для удобства в Monitorado заведены алиасы для наиболее полезных сигналов.
Их названия начинаются с символа `%`.

### Алиасы для сигналов

Все сигналы ниже показывают количество ошибок, удовлетворяющих определенному фильтру, в секунду.
[Документация RUM](https://github.yandex-team.ru/rum/error-counter#голован-yasm).
Тип может иметь следующие значения: `client|uncaught|external|script`.

Алиас | Сигнал | Описание
--------|---------|---------
%errors | div(redirlog-errors.{type}.{project}.{platform}_summ, normal()) | Количество ошибок по типу и платформе
%errors_with_page | div(redirlog-errors_with_page.{type}.{project}.{page}.{platform}_summ, normal()) | Количество ошибок по типу, странице и платформе
%errors_with_block | div(redirlog-errors_with_block.{type}.{project}.{block}.{platform}_summ, normal()) | Количество ошибок по типу, блоку и платформе
%errors_with_source | div(redirlog-errors_with_source.{type}.{project}.{source}_summ, normal()) | Количество ошибок по типу и источнику
%errors_with_source_method | div(redirlog-errors_with_source_method.{type}.{project}.{source}.{source_method}_summ, normal()) | Количество ошибок по типу, источнику и методу источника
%errors_with_environment | div(redirlog-errors_with_environment.{type}.{project}.{environment}.{platform}_summ, normal()) | Количество ошибок по типу, окружению и платформе
%errors_by_service | div(errors_by_service.{type}.{project}.{service}.{platform}_summ, normal()) | Количество ошибок по сервису и платформе
