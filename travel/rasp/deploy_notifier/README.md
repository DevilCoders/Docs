# Deploy Notifier

## Описание
Микросервис на python, который из разных источников получает информацию о статусе сервисов и пишет её в соответствующие тикеты в [startrek](https:://st.yandex-team.ru/).

### Добавление уведомлений в Qloud-приложение
Открываем нужное окружение в Qloud. Например, https://platform.yandex-team.ru/projects/rasp/morda-front/testing – тестинг морды-фронт.

Там переходим на вкладку Policies.

![Policies](https://jing.yandex-team.ru/files/phi191/Screen%20Shot%202018-07-26%20at%2018.29.58.png)

Добавляем нужный адрес в поле Deploy hook и нажимаем Save.

![Deploy Hook](https://jing.yandex-team.ru/files/phi191/Screen%20Shot%202018-07-26%20at%2018.38.49.png)

#### Как получить адрес для хука
Если добавляем Deploy hook в Qloud, то нужно писать следующее:
```
https://production.deploy-notifier.rasp.common.yandex.ru/source/qloud?handlers=<список обработчиков>
```
Обработчики перечисляются через `%2C`. Пока возможных обработчиков два: `startrek` и `telegram`.

Примеры адресов хуков:
* `https://production.deploy-notifier.rasp.common.yandex.ru/source/qloud?handlers=telegram` – будет посылать уведомления только в телеграм
* `https://production.deploy-notifier.rasp.common.yandex.ru/source/qloud?handlers=telegram%2Cstartrek` – будет посылать уведомления и в телеграм, и в startrek

#### Как выбираются тикеты в Startrek
Все тикеты достаются из комментария в Qloud. Поэтому важно деплоить через Teamcity. Если выкатить версию в production руками, то комментария не будет (если вы сами его не напишете), а значит, бот не поймёт, в какие тикеты он должен написать.


### Источники
#### Qloud
Постоянно опрашивает qloud и следит за статусами окружений. Как только статус меняется, получает полную информацию о соответствующем окружении и передаёт её обработчику событий.

#### HTTP
На заданном порту ожидает HTTP POST-запроса на `/` в виде JSON. Как только получает корректный запрос, передаёт его обработчику. Используется в Sandbox. Каждый `RASP_BUILD_AND_RELEASE` присылает информацию о таске.

### Обработчики
#### Log
Просто логирует событие с помощью `logging`.

#### Startrek
Использует шаблоны, написанные на Jinja 2, генерирует описание события и отправляет его в startrek.

#### LoadTesting
Запускает таск в sandbox, передаёт ему название приложения.

## Переменные окружениея
* `STARTREK_LOGIN` – логин бота в стартрек
* `STARTREK_TOKEN` – OAuth токен для доступа к [startrek](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=a7597fe0fbbf4cd896e64f795d532ad2)
* `STARTREK_QUEUES` – список очередей в startrek, в которые нужно отправлять сообщения (например TRAINS,RASPINFRA,RASPFRONT)
* `QLOUD_TOKEN` – OAuth токен для доступа к [qloud](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=072224ad7c864b158601e49b25497eac)
* `TELEGRAM_TOKEN` – токен для отправки сообщений в телеграм
* `TELEGRAM_CHAT_ID` – id чата, в который нужно отправлять сообщения
* `RUN_LOAD_TESTING` – запускать нагрузочное тестирование
* `SANDBOX_TOKEN` – токен Sandbox
* `SANDBOX_OWNER` – Owner, с которым будут запускаться Sandbox-таски
* `SANDBOX_LOAD_TESTING_CONFIG_PATH` – путь до конфига, который передаётся таскуg
