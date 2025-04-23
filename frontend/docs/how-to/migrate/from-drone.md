# Миграции проектов с Drone CI

> Перед миграцией ознакомьтесь с описанием работы [Drone CI в монорепозитории][drone_ci_monorepo_faq].

## Миграция истории репозитория

Создайте пулл-реквест с историей git-репозитория вашего пакета или сервиса.

> Подробнее о миграции git-репозиториев в монорепозиторий frontend [читайте][import_from_git] в отдельном документе.

## Настройка Drone CI 

### Настройка доступов

[Выдайте][docker_role_idm] роль `viewer` к Docker-образам из конфигурации `.drone.yml` для [@robot-frontend].

Docker-образы указаны в полях `image` конфигурации `.drone.yml`.

### Настройка секретов

Основные секреты для работы с Drone уже настроены.

Если для вашего `.drone.yml` нужно добавить секрет, выполните следующие действия:

1. Добавьте секреты в [Sandbox Vault][sandbox_vault] для owner [FRONTEND][frontend_vault].
1. Укажите в описании секрета «Токен для Docker-плагина XXX в Drone».

> Подробнее о хранении секретов в CI читайте в [инструкции][secrets_manual].

### Настройка код-ревью

Удалите из `.drone.yml` команды, отвечающие за код-ревью.

> Для сопровождения код-ревью нужно использовать [devexp]. 

Настройте код-ревью своего проекта в [.devexp.json](../../../.devexp.json).

### Настройка релизов

Настройте отведение релизов с помощью инструментов монорепозитория.

> Подробнее о настройке релизов монорепозитория [читайте](../setup-releases.md) в отдельном документе.

Настройте запуск релизных проверок на событие `tag` в `.drone.yml`. 

Учитывайте, что релизные проверки запускаются при push-событии в ветки вида `release/<service>/<tag>`. Название тега будет взято из названия релизной ветки.

[drone_ci_monorepo_faq]: ../../faq/drone-ci.md
[drone_ci]: https://www.drone.io/
[trendbox_ci]: https://doc.yandex-team.ru/si-infra/trendbox_ci/trendbox_ci.html
[import_from_git]: ../import/from-git.md
[docker_role_idm]: https://idm.yandex-team.ru/#rf=1,rf-role=xn3FIMD8#user:robot-frontend@docker(fields:();params:()),f-status=all,sort-by=-updated,rf-expanded=xn3FIMD8
[@robot-frontend]: https://staff.yandex-team.ru/robot-frontend
[sandbox_vault]: https://sandbox.yandex-team.ru/admin/vault
[secrets_manual]: https://doc.yandex-team.ru/si-infra/trendbox_ci/trendbox_ci_konfiguraciya/trendbox_ci_hranenie_sekretov.html
[frontend_vault]: https://sandbox.yandex-team.ru/admin/vault?owner=FRONTEND&limit=20
[devexp]: https://github.yandex-team.ru/devexp/devexp#%D0%BE%D0%BF%D0%B8%D1%81%D0%B0%D0%BD%D0%B8%D0%B5-%D0%BA%D0%BE%D0%BD%D1%84%D0%B8%D0%B3%D0%B0
