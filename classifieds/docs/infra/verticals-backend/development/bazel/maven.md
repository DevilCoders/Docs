# Интеграция с maven

## Как устроена
TODO: описать:
  - почему сделано так

## Зачем нужен `maven_install.json` в корне
Коммит `maven_install.json` – это способ запинить зависимости, чтобы сборки были детерминированные.
Подробнее в [rules_jvm_external][rules_jvm_external_link].

## Обновление maven зависимостей

Для того чтобы добавить или обновить зависимость необходимо:
  - Добавить/обновить зависимость в файле WORKSPACE (в методе `maven_install` с именем `name = "maven"`)
  - Вызвать `make update/maven`
  - Подождать около минуты
  - Закоммитить `WORKSPACE` и `maven_install.json`

## Неиспользуемые зависимости

Чтобы найти зависимости, которые не используются в проектах, можно запустить команду:
```bash
make unused_deps
```

[rules_jvm_external_link]: https://github.com/bazelbuild/rules_jvm_external#pinning-artifacts-and-integration-with-bazels-downloader
