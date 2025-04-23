# Browser Autofill
Страничка с пользовательскими данными для автоматического заполнения полей ввода в формах.

## Разработка
1. Проверяем, что есть доступы до:
   - addrs-testing.search.yandex.net:(80|443)
   - cloud-api.dst.yandex.net:8443
   - uaas.search.yandex.net:(80|443)
1. Устанавливаем зависимости: `npm i`.
1. Запускаем проект: `npm run local`. \
Локально проект поднимается с использованием тулзы [magicdev](https://wiki.yandex-team.ru/q/devops/magicdev/#readme).
Для корректной работы может понадобится установить сертификат через [сертификатор](https://crt.yandex-team.ru/)
(описано в разделе "Как использовать") для хоста `localhost.msup.yandex.ru`. После получения сертификата, положить его
в корень проекта. \
Обратите внимание, что `magicdev` должен попросить ввести пароль от `sudo`.
Это необходимо, чтобы у процесса был доступ до 443 порта.

1. Открыть проект в браузере можно по двум урлам:
    - https://localhost.msup.yandex.ru/popup?open=1. \
    Версия формы во frame.
    - https://localhost.msup.yandex.ru/bro. \
    Версия для нативного бабла Я.Браузера.
    
Для всех остальных путей сработает редирект в паспорт. Доступны следующие параметры запроса:
- `location` - адрес партнера, где будет открываться автофил. Для тестирования можно использовать `https://sdelano.net/browser/forms/autofill_simple` 
- `_ym_uid` - uid пользователя, передется в abt за экспериментами в куке yandexuid:
  ```
  Cookie: `yandexuid=${req.query._ym_uid}`
  ```
- `theme` - `light` | `dark`
- `fields` - типы полей с данными пользователя, которые нужно показать на странице. Доступны `firstName`, `lastName`, `email`, `phone` и `address`.
Строка в с типами, разделенными запятой. \
Пример: `firstName,lastName,email`.
- `open=1` - параметр, который автоматически откроет форму с данными для автофила. Если его не передать, версия формы во frame не откроется.


для запуска на деве:

- `npm run build` - запуск сборки
- `NODE_TLS_REJECT_UNAUTHORIZED=0 PORT=1118 npm run magicdev -- -p 1117` - 1118 порт на котором запускается нода, 1117 - порт на котором слушаем веб, команда запускает прокси (нужно заменить на nginx)
- `NODE_TLS_REJECT_UNAUTHORIZED=0 PORT=1118 NODE_ENV=development NODE_OPTIONS='--stack-trace-limit=1000' node ./bin/www `
-  `https://localhost.msup.yandex.ru:1117/provider?processName=save&drawer=0&origin=https%3A%2F%2Ftest.sso-test.kinopoisk.ru&open=1`