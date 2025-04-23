## Дока для разработчиков биллинга "Как добавить новый воркспейс"

Если нужно добавить поддержку нового воркспейса, то нужно сделать следующее:

1) Создать секреты с логином/паролем пользователя облака с правами на чтение тестового и продового кластера кликхауса (пример секретов в [тестинге](https://yav.yandex-team.ru/secret/sec-01fxth8mfb1zpb2gzq6t58mjjw) и [проде](https://yav.yandex-team.ru/secret/sec-01fxthbjmxjy2natkh196z8q0t)).
2) Делегировать созданные секреты сервису finstat-api ([дока про делегирование секретов](https://docs.yandex-team.ru/classifieds-infra/deploy/secret)).
3) Добавить конфиги в репозиторий services ([пример pull-request](https://github.com/YandexClassifieds/services/pull/6932)).
4) Добавить воркспейс в код финстаты ([пример pull-request](https://github.com/YandexClassifieds/verticals-backend/pull/9744)).
