# Release Dude Bot

[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=travel/frontend/release-dude-bot&vcs=arc)](https://oko.yandex-team.ru/arc/travel/frontend/release-dude-bot)
[![oko vulnerabilities](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=travel/frontend/release-dude-bot&vcs=arc)](https://oko.yandex-team.ru/arc/travel/frontend/release-dude-bot)

## Описание

Цель проекта - уведомления по релизному циклу

Текущий функционал:

-   отправка информации в чаты `/sendMessage`
-   нотификация о статусах релизов, вызывается в [триггере](https://st.yandex-team.ru/admin/queue/TRAVELFRONT/triggers/45421) ST `/releases/notifyStatus`
-   личное информирование об изменении статуса тикетов `/startrek/issues/:issueId`
-   оповещение о смене дежурств

Для передачи дополнительных параметров можно использовать `query` параметры, например:
`/sendMessage?message=сообщение` – в параметре `messsage` лежит тело сообщения, которое будет отправлено в чат

## Где живет

-   Deploy: https://deploy.yandex-team.ru/stages/travel-frontend-release-dude-bot-production

**ATTENTION**
Бот умеет работать только в единственном экземпляре.
Нет системы оркестрации, если запустить несколько, то будут дублироваться сообщения.

## Настройка

-   [разработка на dev-сервере](docs/remote-dev/remote-dev.md)
-   первым делом нужно создать бота в Telegram через @botfather, получить его токен (будет в ответе от @botfather после создания)
    и положить в переменную `TELEGRAM_TOKEN` в `.env.development`
-   чтобы боту было куда отправлять свои сообщение, нужно добавить его в группу и обратиться к нему какой-нибудь любой командой, например:
    `/help @your-bot-name`, после этого нужно получить id чата и положить его в переменную `TELEGRAM_DUTY_CHAT_ID` в `.env.development` (получить id чата можно, перейдя по ссылке вида `https://api.telegram.org/bot<botToken>/getUpdates`, в массиве results будет объект `chat`, в нём `id`)
-   для авторизации в стартреке и на стаффе нужен OAuth токен, получить его можно [здесь](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5f671d781aca402ab7460fde4050267b), в .env он нужен в переменных `STARTREK_OAUTH_TOKEN` и `STAFF_OAUTH_TOKEN`
