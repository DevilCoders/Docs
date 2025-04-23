# Hermione Тесты для проекта Pay для внешних мерчантов

Набор e2e и UI тестов, необходимых для проведения рефакторинга и переработки кодовой базы. В перспективе
для запуска в ci.

##Требуются:

nvm или установленный в окружении Node.js 12.18.0 с npm.

## Быстрый старт
```bash
git clone git@github.yandex-team.ru:Billing/yandex-pay.git
cd yandex-pay/hermione
npm install
npm run test:gui
```

## Запуск тестов
* `npm run test` — запуск тестов с результатом в консоли
* `npm run test:gui` — запуск тестов с GUI
  Тесты запускаются в гриде, отчет открывается сразу локально в браузере. Для перезапуска теста
  нажать rerun для нужного теста в ui отчета.
*  для дебага гермионы: https://github.com/gemini-testing/hermione#debug 

Тесты ходят по урлу на https://test.pay.yandex.ru/demo . 
Все карты и юзеры в тестах - должны быть тестовые.

## Использыемые плагины и библиотеки
Для логина пользователя в браузере используется плагин [hermione-auth-commands](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/hermione-auth-commands)
Этот плагин использует [TUS](https://wiki.yandex-team.ru/test-user-service/#sozdaniekonsjumera), но не предоставляет апи для получения пароля или токена для логина 
пользователя. Но пароль или токен нужен для привязки карт.
Поэтому для этого в тестах используется непосредственно сам TUS-клиент. 
Для отправки запросов на привязку/отвязку карт используется [Мобильное Апи](https://wiki.yandex-team.ru/trust/mobileapi/#bindcard) и
библиотека [axios](https://github.com/axios)

## Структура проекта
* Тестовые данные — `config/test-data.js`
* Подготовка залогина юзера и получение токена/пароля - `helpers/get-auth.js`
* Привязка карты к пользователю - `helpers/bind-card.js`

Сами тесты лежат в '/tests'. 
Пока идея такая: сделать там 3 папки в соответствии с 
приоритетными сьютами в Testpalm: acceptance, business logic, regress.
В каждой такой папке будут выделены скриншотные тесты и остальгные тесты по фичам.
ToDo: обсудить!

## Список бруазеров и что тестируем
Шаблоны — `desktop` и `mobile`

## Устранение проблем
В случае непонятных проблем при установке зависимостей или сборке следует попробовать почистить node_modules:
```
rm -rf node_modules
npm install
```

[hermione-auth]: https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/hermione-auth-commands
