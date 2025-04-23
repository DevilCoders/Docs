# Новый календарь
![npm stable version](https://badger.yandex-team.ru/npm/@ps-int/maya/version.svg)
![npm beta version](https://badger.yandex-team.ru/npm/@ps-int/maya/version.svg?tag=beta)
[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=yandex360/frontend/services/maya&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/services/maya)
[![oko health](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=yandex360/frontend/services/maya&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/services/maya)

Maya - это фронтенд календаря с 2016 года.

Содержит клиентскую статику и stateless динамику (серверную часть).

Разработка ведётся в очереди [Maya](https://st.yandex-team.ru/MAYA)

Статика построена на стеке [React](https://github.com/facebook/react)+[Redux](https://github.com/reactjs/redux)+[Redux-Saga](https://github.com/redux-saga/redux-saga). Собирается с помощью webpack, тестируется с помощью [Jest](https://github.com/facebook/jest)

Выкатывается на s3://mail/maya.

Поддерживает совместимость со следующими [браузерами](docs/browser-compability.md)

## Динамика
Динамика построена на базе http сервера [duffman](https://github.yandex-team.ru/Daria/duffman/wiki).
С использованием NodeJS 14.16+.<br>
Выкатывается в qloud

## Для разработчика:

- [Инструкция по запуску](docs/qyp.md)
- [Соглашения по коду](docs/code-style.md)
- [Работа с текстами](docs/texts.md)
- [Инструкция по сборке проекта](docs/duty/package.md)

## Графики

* [Основной дашборд maya](https://yasm.yandex-team.ru/panel/pistch.maya_public_brief/)
* [MODEL_REJECTED maya](https://yasm.yandex-team.ru/panel/pistch.maya_public_model-rejected/)

* [Основной дашборд maya-corp](https://yasm.yandex-team.ru/panel/pistch.maya_corp_brief/)
* [MODEL_REJECTED maya-corp](https://yasm.yandex-team.ru/panel/pistch.maya_corp_model-rejected/)

* [RUM desktop](https://stat.yandex-team.ru/Dashboard/User/3y3k0/MailSpeed?tab=1000j&state=6FvaVCiC6MLl#calendar:calendar.desktop)

## Клиентские ошибки

* [error booster](https://error.yandex-team.ru/projects/maya)
* [yasm](https://yasm.yandex-team.ru/panel/fresk._ODOtva/)

## Облако (Qloud)

* [maya](https://qloud-ext.yandex-team.ru/projects/mail/maya)
* [maya-corp](https://qloud-ext.yandex-team.ru/projects/mail/maya-corp)

## Счётчики Яндекс.Метрики

|  **Calendar v2** |          |
| ----------       | -------- |
| dev              | 42367769 |
| corp-touch       | 50533030 |
| corp-desktop     | 45227700 |
| public-touch     | 50533015 |
| public-desktop   | 42367379 |

|  **Calendar v1** |          |
| ----------       | -------- |
| corp             | 1785466  |
| public           | 2105797  |
