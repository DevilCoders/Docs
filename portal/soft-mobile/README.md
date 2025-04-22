# soft-mobile [mobile5-www]

[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=browser/frontend/soft-mobile&vcs=arc)](https://oko.yandex-team.ru/arc/browser/frontend/soft-mobile)

- [soft-mobile [mobile5-www]](#soft-mobile-mobile5-www)
  - [Подготовка](#подготовка)
  - [Установка и запуск](#установка-и-запуск)
  - [Окружение](#окружение)
  - [Ссылки](#ссылки)

## Подготовка

Для работы потребуется Node.js v14. Рекомендуется для выбора версии Node.js
использовать [NVM][nvm].

[nvm]: https://github.com/nvm-sh/nvm

```bash
nvm install

# В репозитории используется package-lock.json с lockfileVersion равным 2.
# Желателен минимум npm v7
npm install -g npm@latest
```

## Установка и запуск

Значение секретов можно узнать в [Секретнице][yav].

[yav]: https://yav.yandex-team.ru/secret/sec-01ehphp8d1d99nr4fdyt8fbkwf

```bash
# Устанавливаем зависимости
npm install

# Генерируем tvm.json.
# Пробел перед командой предотваращает попадание команды в ~/.zsh_history,
# если в шелле включена HIST_IGNORE_SPACE (man zshoptions)
 CLIENT_SECRET=<значение секрета> npm run tvm:init

# Запускаем dev server
npm run dev
```

Проект становится доступен по адресу:
https://localhost.msup.yandex.ru:8443/

## Окружение
| Ключ                              | Описание                                           |
| --------------------------------- | -------------------------------------------------- |
| APP_VERSION                       | Устанавливается билд системой                      |
| CHECK_TOKEN_REQUEST_IP_MATCH      | Проверка IP получения токена с IP запроса на ручку |
| CSRF_KEY                          | [express-csrf][github-express-csrf]                |
| HTTP_PORT                         | Порт приложения                                    |
| LOG_LEVEL                         | [Уровень логгирования][arc-yandex-logger]          |
| NODE_ENV                          | Тип окружения production/development               |
| NUMBER_PREFIX_FILTER              | Список забаненных префиксов через запятую          |
| REQUESTS_LIMIT_EMAIL              | EMAIL в минуту на один IP                          |
| REQUESTS_LIMIT_SMS                | SMS в минуту на один IP                            |
| TOKEN_CAPTCHA_CLIENT              | [Клиентский токен SmartCaptcha][wiki-smartcaptcha] |
| TOKEN_CAPTCHA_SERVER              | [Серверный токен SmartCaptcha][wiki-smartcaptcha]  |
| TVMTOOL_LOCAL_AUTHTOKEN           | [Токен для TVM демона][wiki-tvm-daemon]            |
| VERY_BAD_CHECK_DONT_USE_IS_ACTIVE | Плохая проверка номеров (RU, UA, BY, TR)           |

[arc-yandex-logger]: https://a.yandex-team.ru/arc_vcs/frontend/packages/yandex-logger#urovni-logirovaniya
[github-express-csrf]: https://github.yandex-team.ru/soft/express-ycsrf
[github-yandex-csrf]: https://github.yandex-team.ru/maps-legacy/csrf
[wiki-smartcaptcha]: https://wiki.yandex-team.ru/jandekspoisk/sepe/antirobotonline/captcha/#connect
[wiki-tvm-daemon]: https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/#kakzapustitprocess

## Ссылки

* [Error Counter](https://error.yandex-team.ru/projects/soft-mobile/)

> Powered by [Reactive-Stub](https://github.yandex-team.ru/reactive-stub/generator-reactive-stub) v1.3.1 and unicorns
