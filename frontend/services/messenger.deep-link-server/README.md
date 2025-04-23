# Сервер диплинков пользователей staff

## Сборка

### Trendbox CI

При наличии изменений автоматически собираются докер-образы:
- из ПР: registry.yandex.net/messenger-frontend/deep-link-server:vX.X.X-pull-NNNN
- из dev: registry.yandex.net/messenger-frontend/deep-link-server:vX.X.X-dev-YYYYYYYY
- из релиза: registry.yandex.net/messenger-frontend/deep-link-server:vX.X.X

## Деплой

Настроен автоматический деплой:
- ~~из ПР: в test-corp~~
- ~~из дев: в test-corp, internal-dev~~
- ~~из релиза: в internal-prod~~

Окружения:

| Окружение | Версия | Qloud | Logs | Dashboard |
| --- | --- | --- | --- | --- |
| internal-prod | ![Версия](https://badger.yandex-team.ru/qloud/mssngr/yamb-web/internal-prod/deep-link/version.svg) | [Qloud](https://platform.yandex-team.ru/projects/mssngr/yamb-web/internal-prod) | [Logs](https://platform.yandex-team.ru/projects/mssngr/yamb-web/internal-prod?tab=logs-beta) | [Dashboard](https://platform.yandex-team.ru/projects/mssngr/yamb-web/internal-prod?tab=dashboard) |
| internal-dev | ![Версия](https://badger.yandex-team.ru/qloud/mssngr/yamb-web/internal-dev/deep-link/version.svg) | [Qloud](https://platform.yandex-team.ru/projects/mssngr/yamb-web/internal-dev) | [Logs](https://platform.yandex-team.ru/projects/mssngr/yamb-web/internal-dev?tab=logs-beta) | [Dashboard](https://platform.yandex-team.ru/projects/mssngr/yamb-web/internal-dev?tab=dashboard) |
| test-corp | ![Версия](https://badger.yandex-team.ru/qloud/mssngr/yamb-web/test-corp/deep-link/version.svg) | [Qloud](https://platform.yandex-team.ru/projects/mssngr/yamb-web/test-corp) | [Logs](https://platform.yandex-team.ru/projects/mssngr/yamb-web/test-corp?tab=logs-beta) | [Dashboard](https://platform.yandex-team.ru/projects/mssngr/yamb-web/test-corp?tab=dashboard) |
