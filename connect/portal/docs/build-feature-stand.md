## Сборка окружений для тестирования отдельных фич
На данный момент версия докер образа, также как и название окружения с которым идет работа, равны имени текущей ветки в git.

Для использования данного скрипта требуется установленный [релизер](https://github.yandex-team.ru/tools/releaser)

### Установка releaser с помощью [pip](https://pip.pypa.io/en/stable/installing/)

Установка зависимостей для всех команд:

`pip install -i https://pypi.yandex-team.ru/simple/ releaser-cli[all]`

После установки пропишите переменную `oauth_token` в `~/.release.hjson`. Ее значением должен быть oAuth токен, связанный с пользователем, который имеет права на работу с указанным Qloud окружением. [Получить токен](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1).

##### Пример файла
`oauth_token: AQAD-qJSJiQqBxX9VPVMkBBD1vdvfCvvBTdIi1E`

### Создание окружения из текущей ветки
`./feature-stand.sh`

Состоит из:
- сборка образа
- создание окружения
- добавление в окружение домена

### Обновить окружение из текущей ветки
`./feature-stand.sh --update`

Состоит из:
- сборка образа
- обновление версии образа на стенде

### Удаление окружение с именем текущей ветки
`./feature-stand.sh --delete`

### Сборка docker-образа с именем ветки в качестве имени
`npm run feature`
