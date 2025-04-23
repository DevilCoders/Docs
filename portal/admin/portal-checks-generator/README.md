## Генератор активных и хостовых проверок всех сервисов Главной страницы
### Установка juggler-sdk

`pip3 install --index-url https://pypi.yandex-team.ru/simple juggler-sdk`

https://juggler-sdk.n.yandex-team.ru

### Запуск
Получить токен [здесь](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=cd178dcdc31a4ed79f42467f2d89b0d0)

`export JUGGLER_OAUTH_TOKEN=<YOUR_TOKEN>` 

`./run.sh`
