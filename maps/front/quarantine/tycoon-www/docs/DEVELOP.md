### Как начать разрабатываться

1. Идем в репозиторий https://a.yandex-team.ru/projects/maps-front-tycoon/code/maps/front/quarantine/tycoon-www
2. Устанавливаем зависимости `npm сi`
3. Устанавливаем конфиг (см. пункт "Конфиги при разработке на localhost")
4. Запускаем в отдельной вкладке проекта в терминале автоперезапуск сервера `npm run dev`
5. Открываем в браузере `http://localhost:8082/`

* Если нужно разрабатывать какой-то отличный от index бандл, запускаем сервер командой `REBUILD_BUNDLE=landing npm run dev`

#### Договоренности

Используем следующие версии:
* Node.js – v12.20.*
* npm – 6.4.*

Указываем [переменные окружения](https://clubs.at.yandex-team.ru/devtools-frontend/559) в `.bashrc`/`.bash_profile`/`.zsh`
```bash
export NVM_NODEJS_ORG_MIRROR=https://nodejs-mirror.s3-website.mds.yandex.net/dist
export npm_config_disturl=https://nodejs-mirror.s3-website.mds.yandex.net/dist
export PHANTOMJS_CDNURL=http://download.cdn.yandex.net/phantomjs
```

Устанавливаем:
```bash
$ nvm install 12.20
```

Выполняем `nvm use` в директории проекта, чтобы выбрать версию ноды.

Или включаем нужную версию по умолчанию:
```bash
$ nvm alias default 12.20
```

### Доступы
1. Tanker: Запросить роль https://idm.yandex-team.ru/#rf-role=ntwODOkL#tanker/projects/tycoon-www/common/Developer;;;,rf-expanded=ntwODOkL,rf=1.
2. Docker: Надо получить токен [Токен](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1). После чего залогиниться через терминал `docker login  -u <login> -p <token_body> -e <email>@yandex-team.ru registry.yandex.net`. И запросить доступ в репозиторий в [управляторе](https://idm.yandex-team.ru/#main=roles,sort-by=-updated,f-status=all,rf=1,rf-role=docker/distribution/tycoon%7Cfrontend/contributor,rf-scope=docker/distribution/tycoon%7Cfrontend).
3. Доступ к тестингу https://nda.ya.ru/3UtYLK
4. Доступ к проду https://nda.ya.ru/3UtYX3

### Конфиги при разработке на localhost
Для использования локальных конфигов, необходимо добавить `export YANDEX_ENVIRONMENT=local` в `.bashrc`/`.bash_profile`/`.zsh`.

При разработке на `localhost` локальный конфиг будет пытаться подключить неверсионируемый файл `configs/local/local.js`, из которого можно экспортировать приватные данные:
```js
module.exports = {
    uid: 1122334455, // Заменить на свой uid, который можно получить из урла, например, почты https://mail.yandex.ru/
    requestOptions: { timeout: 2000, retry: 1 },
    debug: true,
    tvm: {
        serverUrl: 'http://localhost:8001',
        timeout: 1000,
        token: '***' // где *** - секрет  https://nda.ya.ru/t/r9ym1CQy4eZxbS
    }
};
```

### Локальный запуск тестов
1. Запросить роль https://nda.ya.ru/t/tCR0D_po5FLHVH
1. Сделать экспорт в локальных переменных `export HERMIONE_OAUTH_TOKEN=<token>`, где token можно получить по ссылке https://nda.ya.ru/t/oS7IIVYz5FLKkR

### Выгрузка переводов из Танкера
Проект в [танкере](https://tanker.yandex-team.ru/project/tycoon-www).
Выгрузка переводов не требует токен, но, если вдруг переводы перестанут скачиваться, нужно получить токен по ссылке https://nda.ya.ru/3SjQY7 и добавить его в свою переменную окружения `TANKER_API_TOKEN`.

#### Работа с переводами в БЭМ-стеке
- использовать нужный ключ в коде
- вручную добавить ключ в кейсет в интерфйсе Танкера: добавляем только русский перевод, выставляем статус "подтверждено"
- в проекте запустить `tanker pull`

#### Работа с переводами в react-стеке
- использовать перевод в коде
- в проекте запустить `tanker sync`

### Дебаг:

#### Обработка ручек с ошибками
Бэк нам сделал ручку `/admin/echo`, которая умеет отдавать любой статус и таймаут.
Пример использования: `tycoon.admin.echo(req, { status: 500, timeout: 5000 } ).catch(() => {})`.
Ручка работает только в тестинге и престейбле.

### Флаги экспериментов
Флаг эксперимента можно прокинуть через query-параметр `expFlags=show_main,show_coll_link`.
Можно перечислить несколько экспериментов через запятую или точку с запятой.
Проброс параметров работает на всех окружениях, но в проде доступен только для яндексовых аккаунтов, которые привязаны на staff.

#### Для локальной разработки на https
- Нужно добавить в `/etc/hosts` запись `127.0.0.1 localhost.sprav.yandex.ru`
- Запуск: `npm run dev:https`
- В браузере сервис будет доступен под урлом `https://localhost.sprav.yandex.ru:8082/`

#### Для локальной разработки с tvm-тикетами
- Запрость роль Разработчика https://nda.ya.ru/t/NcBg6Dmq57zEtM (нужен для прокси блэкбокса, который живет на master.beta)
- Нужно добавить в `/etc/hosts` запись `127.0.0.1 localhost.sprav.yandex.ru`
- Локально заэкспортить переменную `export TVMTOOL_LOCAL_AUTHTOKEN=***`, где *** - секрет окружения
 tycoon-frontend-testing, который можно взять в секретнице https://nda.ya.ru/t/r9ym1CQy4eZxbS
- Запуск: `npm run dev:tvm`;
- В браузере сервис будет доступен под урлом `https://localhost.sprav.yandex.ru:8082/`

#### Запуск локальной публичной беты
- Команда `npm run dev:public`;
- Или если нужен другой режим запуска, то добавляем переменную окружения `PUBLIC=1`

### Добавление переводов
* Настроен процесс создания автотикетов на новые ключи в танкере
* [Процесс в Hitman](https://hitman.yandex-team.ru/projects/sprav_frontend/tycoon_frontent_autoticket/)
* [Гайд по настройке](https://wiki.yandex-team.ru/l10n/tools/translate-autoticket-v2/)
* [Форма для заказа переводов вручную](https://forms.yandex-team.ru/surveys/13067/)

### Добавление компании в "Мои компании"
1. Перейти по урлу `/search` и найти любую компанию
2. Нажать на название компании
3. В открывшемся блоке нажать на кнопку "Это моя компания"
4. Ввести любое контактное лицо и нажать "Получить код"
5. Нажать на кнопку "Открыть "Заявки на подтверждение""
6. Нажать "Ввести код"
7. Ввести код `0123`

### Просмотр страниц на разных языках
1. В local.js в массиве langs должны быть требуемые для сборки языки
2. В урле параметром можно передать язык для отображения `&lang=tr`

### Важное
- все ссылки, которые ведут на документацию 'https://yandex.{tld}/support/sprav', должны открываться в новой вкладке.
- используем общепортальные иконки https://depot.yandex-team.ru/search/icons/

### [React](./REACT.md)

### Счетчики
* Запросить доступ - http://idm.yandex-team.ru/ -> Метрика -> Доступ к счетчику -> Идентификатор счетчика: 39321485
* Заходим в [метрику](https://metrika.yandex.ru/dashboard?group=day&period=week&id=39321485) -> Настройка -> Цели -> Добавить цель
* Поля:
  * Название: Описание события по какой-то кнопке или ссылке. Например, "Клик по кнопке 'Данные актуальны'"
  * Тип условия: JavaScript-событие
  * Идентификатор цели: Большими латинскими буквами через нижнее подчеркивание цель для метрики. Например, DATA_IS_ACTUAL_CLICK
* Клик - "Добавить цель"

### Разработка отображения панорам
Для доступа к карточному апи панорам нужен `apikey`.
Он был создан под внешним логином команды: login `tycoon-sprav`, пароль https://nda.ya.ru/t/sLIxw_823gv3By, [по инструкции](https://wiki.yandex-team.ru/maps/api/enterprise/keys/#jsapi).
Для локальной разработки нужно получить `apikey` в секретнице (https://nda.ya.ru/t/_xgIh8Ch3gv3hK) и положить его в локальную переменную `export MAPS_API_KEY=`
Данная переменная также добавлена во все окружения в Deploy.

### z-index
Стараемся использовать 4 уровня приоритета для z-index:
* `--z-index-minimum: 1;` - мелкие элементы, часто `position: absolute` относительно контента блока (например, крестик закрытия окна)
* `--z-index-medium: 100;` - средние элементы, которые нужно выдвинуть на первый план (например, всплывающее окно с подсказкой)
* `--z-index-high: 1000;` - блоки, которые должны перекрывать контент родителя (например, паранджа, попап)
* `--z-index-maximum: 10000;` - важные, большие элементы, которые должны быть всегда выше всех остальных (например, основная шапка, попап с просмотром фотографии)
