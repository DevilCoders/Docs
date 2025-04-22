<!-- # Настройка CI

В директории `/frontend/projects/maps` используется [Trendbox CI](https://doc.yandex-team.ru/si-infra/trendbox_ci/trendbox_ci.html) для CI/CD-задач.

> :warning: CI для каждого пакета или сервиса настраивается отдельно. Изменения в несколько пакетов или сервисов не поддерживаются.

## Настройка Trendbox CI

### Запрос на подключение нового пакета в Trendbox CI

Перед настройкой Trendbox CI напишите в канал [maps-to-frontend](https://yndx-infra.slack.com/archives/C01G2NF62R0) в [slack](https://wiki.yandex-team.ru/slack/).

Укажите путь к директории npm-пакета внутри `/frontend/projects/maps` для подключения к CI. Дождитесь подключения директории.

> На данный момент Trendbox CI не поддерживает автоматическое подключение директорий Аркадии. Поддержка будет реализована в задаче [FEI-20907](https://st.yandex-team.ru/FEI-20907).

### Настройка проверок Trendbox CI

1. Создайте ревью-реквест с пустым `.trendbox.yml` в директории npm-пакета и влейте его.
1. Создайте ревью-реквест с настроенным `.trendbox.yml`. В этот момент запустятся проверки, согласно конфигурации, добавленной в текущем ревью-реквесте.

> На данный момент Trendbox CI не поддерживает запуск при добавлении нового `.trendbox.yml`. Поведение будет исправлено в задаче [FEI-21370](https://st.yandex-team.ru/FEI-21370).

### Настройка секретов

[Создайте](https://doc.yandex-team.ru/si-infra/trendbox_ci/trendbox_ci_konfiguraciya/trendbox_ci_hranenie_sekretov.html#sozdanie-sekreta) секрет `env.ARCANUM_API_OAUTH_TOKEN` для вашей [Sandbox-группы](https://doc.yandex-team.ru/si-infra/trendbox_ci/trendbox_ci_konfiguraciya/trendbox_ci_hranenie_sekretov.html#sozdanie-gruppy).

> О том как получить токен для Arcanum читайте в [документации](https://wiki.yandex-team.ru/arcanum/api/#avtorizacijachereztoken).

[Создайте](https://doc.yandex-team.ru/si-infra/trendbox_ci/trendbox_ci_konfiguraciya/trendbox_ci_hranenie_sekretov.html#sozdanie-sekreta) секрет `env.ARC_TOKEN` для вашей [Sandbox-группы](https://doc.yandex-team.ru/si-infra/trendbox_ci/trendbox_ci_konfiguraciya/trendbox_ci_hranenie_sekretov.html#sozdanie-gruppy).

> О том как получить токен для `arc` читайте в [документации](https://doc.yandex-team.ru/arc/setup/arc/install.html#oauth-token).

## Настройка Arcanum

Создайте файл `a.yaml` в директории npm-пакета.

1. Укажите abc-сервис в качестве владельца npm-пакета.
1. Укажите названия проверок от Trendbox CI.

```yaml
service: package-abc-service
title: My Package

arcanum:
  auto_merge:
    enabled: false

    requirements:
      - system: ci/trendbox
        type: "ci/trendbox [test]: unit"
        need_disable_reason: true
```

## Настройка ревью

1. Создайте ревью-реквест с настроенным [.devexp.json](https://github.yandex-team.ru/devexp/devexp) в директорию npm-пакета и влейте его.
1. Дождитесь пока файл появится в [индексе](https://a.yandex-team.ru/search?search=,.devexp.json,,arcadia,,500&repo=) Аркадии.

> Настройки ревью всегда будут взяты из `trunk`, даже если вы изменяете `.devexp.json` в ревью-реквесте. -->
TODO