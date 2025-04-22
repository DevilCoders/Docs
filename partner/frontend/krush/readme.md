krush
=====

<img src="king-krush.jpg">

Сервис, позволяющий работать с [вебхуками](https://developer.github.com/enterprise/2.4/webhooks/) и выполнять определенные действия в ответ на соответвующие события.

## Требования

Для работы с [github API](https://developer.github.com/v3/) и автоматизации проведения ревью через [protected branches](https://help.github.com/articles/about-protected-branches/) нужно предоставить [OAuth](https://developer.github.com/v3/oauth/#scopes) токен с правами:
- `repo:status`,
- `public_repo`,
- `read:org`.

Также нужно не забыть выдать право на запись для роботного пользователя к конкретному репозиторию.

Также, в настройках вашего репозитория, нужно указать куда слать [события](https://developer.github.com/enterprise/2.4/webhooks/#events). Стоит указывать путь к ручке `/webhooks`. Например, `https://king.krush/webhooks`.

## Настройка

Базовая информация описана в файле [package.json](package.json) в директиве `config`. Подробнее:

- `githubToken` — переменная окружения, содержащая OAuth токен для github,
- `startrackToken` — переменная окружения, содержащая OAuth токен для startrack,
- `servant` — логин роботного пользователя (не участвует в голосовании),
- `repo` — связывает репозитории с командой, которая проводит ревью,
- `teams` — белый список команд, которые участвую в ревью пулл-реквестов (если пустой список — то все),
- `workers` — количество воркеров (масштабирование приложения).

**Важно**. Для успешной работы нужно передать *oauth* токены для *github'а* и *startrack'а* через соответствующие переменные окружения.
Для работы автозапуска скриншутера необходимо передать авторизационные данные робота,
запускающего скриншутер и пользователя ПИ, под которым ходит скриншутер. Пароль
и того и другого https://yav.yandex-team.ru/secret/sec-01ds082m687k8b87m2tf3cb3s4/explore/versions

## Деплой

Сервис живет в [https://qloud.yandex-team.ru/](https://qloud.yandex-team.ru/) и деплоится через кокаиновый реджистри внутри докерного образа. Осуществляется это следующими командами:

**Важно**: перед деплоем всегда нужно обновлять версию в [package.json](package.json).

Сборка образа:

```bash
$ npm run build
```

Отправка образа в *registry.yandex.net*

```bash
$ npm run push
```

После этого нужно передеплоить [стейдж](https://deploy.yandex-team.ru/stage/krush)
Для этого лучше воспользоваться утилитой [dctl](https://wiki.yandex-team.ru/deploy/docs/tools/dctl/?from=%2Fdeploy%2Fdocs%2Fscenarii-ispolzovanija-dctl%2F):
    `ya tool dctl stage put deploy/spec/krush.yaml` - если находимся в корне проекта krush
Если не получается, в крайнем случае можно зайти в интерфейс деплоя, открыть конфиг
стейджа на редактирование, изменить тэг образа в конфиге бокса, сохранить и передеплоить стейдж.

В конце надо незабыть закоммитить изменения версии в package.json и соответствующего тэга
в deploy/spec/krush.yaml в репозиторий (в конечном итоге в `master`).


## Дополнительная информация

Перевод задач "В работе" -> "Код ревью" и линковка задач в startrack с pr github осуществляется средствами [интеграции startrack с github](https://wiki.yandex-team.ru/tracker/vodstvo/GitHub/#perevodvstatuspriprikrepleniikod-revju)
