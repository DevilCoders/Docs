#### Подготовка

Для работы и тестов нужен env CONDUCTOR_OAUTH_TOKEN. Токен можно взять [тут](https://wiki.yandex-team.ru/conductor/api/#autentifikacija).
Для тестирования локально должен быть установлен terraform >= 0.12.

#### Сборка и тестирование 
Для сборки используется команда `go build -o terraform-provider-conductor`. 
Перед тестированием нужно собрать provider и сделать `terraform init`.
Для ручных тестов пока нет нормальных можно использовать main.tf.  