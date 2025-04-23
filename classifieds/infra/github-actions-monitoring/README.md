# github-actions-monitoring

Github-actions-monitoring - сервис, предназначенный для мониторинга Github Actions. 

Переменная окружения `_DEPLOY_LAYER` помогает отличить dev-окружение от окружения тестинга и прода. Если `_DEPLOY_LAYER` - пустое значение (разработка ведется локально), в корне проекта должен лежать файл `dev.env` с переменными окружения; если это тестинг или прод - переменные окружения должны быть переданы при запуске контейнера:
* `GITHUB_KEY` - приватный ключ Github App'а actions-monitoring в base64. Можно взять [тут](https://yav.yandex-team.ru/secret/sec-01fg45pfypgagf5f9h9dr0jn0n/explore/versions)
* `ROBOT_OPTIMUS_TOKEN` - OAuth-токен робота robot-vertis-repo для похода в StarTrek API.
* `EXCLUDE_LIST` - список исключений для репозиториев, в которых в рамках конвенций/договоренностей проверка не проводится.
Например: `EXCLUDE_LIST=scandex,alien,jaeger,ts-proto,journal-frontend,yav-resolver,journal-adminv2,coverage-github-action`

На текущий момент сервис получает список воркфлоу с соответствующими репозиториями на Github, которые используют внешние гитхаб-раннеры и создает тикет в очереди VERTISADMIN с данным списком.