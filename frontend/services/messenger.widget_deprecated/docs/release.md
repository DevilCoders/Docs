# Процесс релиза виджета

## Отведение релиза

Отвод релиза осуществляется через форму: https://forms.yandex-team.ru/surveys/50569/?service=messenger.widget_deprecated

После нажатия кнопки отвод, создается Sandbox-задача, найти которую можно по этой ссылке: https://sandbox.yandex-team.ru/tasks?children=true&author=robot-frontend&hints=form_50569&owner=FRONTEND&tags=SEARCH-INTERFACES%2FFRONTEND%2CMESSENGER.WIDGET&type=TRENDBOX_CI_JOB&all_tags=true&limit=20

Если задача прошла успешно, то создается тикет в очереди SEAREL: https://st.yandex-team.ru/issues/?_f=type+priority+key+summary+description+status+resolution+created+updated+assignee+tags+parent&_q=Queue%3A+SEAREL+AND+Tags%3A+messenger-widget-deprecated+%22Sort+By%22%3A+Created+DESC

В тикете запускаются все скрипты сборки нового релиза.

## Деплой релиза

После всех проверок, когда можно катить виджет, выкатка происходит в ручную.

Для деплоя должны быть:
- переменная окружения с ключом для стартрека **STARTREK_TOKEN** (получить можно [здесь](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5f671d781aca402ab7460fde4050267b))
- ключи для S3 (см. [использование aws-cli](https://wiki.yandex-team.ru/mds/s3-api/s3-clients/#nastrojjkaawscli)) из [секретницы](https://yav.yandex-team.ru/secret/sec-01d7pn60wk8eg5kn3pgrms4exw/explore/versions)
- ключ для infra.yandex-team.ru

Общая команда для их получения и деплоя выглядит так (запускается в папке сервиса):

```bash:
npm run release
```

Полная подмена скриптов происходит в течение часа.

Ссылки на скрипты на S3:
- https://chat.s3.yandex.net/widget.js
- https://chat.s3.yandex.net/widget_ya.js
- https://chat.s3.yandex.net/widget_ya_internal.js
- https://chat.s3.yandex.net/widget_light.js

Ссылки на скрипты с версией на S3 (заменить 1.X.0 на текущую версию):
- https://chat.s3.yandex.net/1.X.0/widget.js
- https://chat.s3.yandex.net/1.X.0/widget_ya.js
- https://chat.s3.yandex.net/1.X.0/widget_ya_internal.js
- https://chat.s3.yandex.net/1.X.0/widget_light.js

Ссылки на скрипты с версией на yastatic.net (заменить 1.X.0 на текущую версию):
- https://yastatic.net/s3/chat/1.X.0/widget.js
- https://yastatic.net/s3/chat/1.X.0/widget_ya.js
- https://yastatic.net/s3/chat/1.X.0/widget_ya_internal.js
- https://yastatic.net/s3/chat/1.X.0/widget_light.js

## Откат релиза

Производится в ручную, указав ту версию, на которую нужно откатить в переменной окружения VERSION.

Для того, что бы откат произошел, эта версия должна быть ранее задеплоена в https://yastatic.net/s3/chat/$VERSION/

```bash:
VERSION=X.X.X npm run rollback
```

## Зависимости и секреты

- **STARTREK_TOKEN** - oauth токен робота, который дает доступ к Трекеру. Получается [здесь](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5f671d781aca402ab7460fde4050267b)

- **AWS_ACCESS_KEY_ID** и **AWS_SECRET_ACCESS_KEY** - токены доступа к S3 до бакетов messenger-test и chat
