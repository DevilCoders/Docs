[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=yandex360/frontend/packages/service-worker/service-worker-manager&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/packages/service-worker/service-worker-manager)
[![oko health](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=yandex360/frontend/packages/service-worker/service-worker-manager&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/packages/service-worker/service-worker-manager)

## ServiceWorker Manager
Модуль помогает регистрировать сервис воркеры.
<br>
Под капотом подключен [channel-rpc](/packages/channel-rpc) для общения с воркерами по postMessage.

### Параметры инициализации
`config.url` - относительный url инициализации воркера. По умолчанию `/service-worker`.
<br>
`config.scope` - неймспейс в котором будет работать воркер. По умолчанию `/`.
<br>
