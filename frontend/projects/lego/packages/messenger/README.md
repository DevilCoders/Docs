**Блок `messenger` устарел и не поддерживается, используйте [виджет чатов](https://github.yandex-team.ru/serp/chat/tree/dev/services/widget-loader).**


# Блок `messenger`
Иконка Q в шапке со счётчиком непрочитанных сообщений. При клике по иконке отображается попап с мессенджером.

### Состав
* `__box` - контейнер для иконки и счётчика.
* `__icon` – иконка.
* `__popup` — `popup2`, в него кладётся iframe с Q.
* `__spin` - индикатор загрузки.
* `__ticker` — счётчик непрочитанных сообщений, можно задать через `bemjson`.

## Модификаторы
* `size` - размер иконки. Доступные значения: `s`, `m`.
* `internal` - использовать внутренние `yandex-team` ручки. Доступные значения: `yes`.
* `popupType` - тип попапа с мессенджером. Работает только в React-версии. Доступные значения: `popup`, `modal`. По умолчанию: `popup`.
* `tickerType` - тип счетчика непрочитанных. Работает только в React-версии. Доступные значения: `counter`, `dot`. По умолчанию: `counter`.

### Принцип
При инициализации блок подключает [скрипт-загрузчик(Atom)](https://github.yandex-team.ru/lego/islands/tree/4f2a26569d6606f475680a85c9cf8879d563dda9/packages/iframe-loader), вставляет в попап iframe с Q и устанавливает RPC-мост, через который ЦУ вызывает методы блока, а блок методы ЦУ. Когда ЦУ получает данные о сервисах из своей ручки, он дёргает через мост метод `onDataLoad` и `spin2` заменяется ЦУ.

#### Как инициализируется ЦУ:
При инициализации `messenger` грузится скрипт `iframe-loader`, который грузит страницу `global-notifications` и вызывает `onIframeLoad` в `messenger` после загрузки `iframe`. В `onIframeLoad` внутрь `iframe` кидается `postMessage` с параметрами подключения к БД и белый экран в `iframe` меняется на загруженные уведомления.

### JS-параметры
* `serviceId` - идентификатор сервиса. Услуги: 1, Поиск: 2, Районы: 3.
* `loaderUrl` - iframe-загрузчик. По умолчанию: `https://yastatic.net/q/global-notifications/iframe-loader/stable/index.min.js`,
* `iframeUrl` - урл iframe мессенджера. По умолчанию: `https://yandex.ru/chat?build=chamb`
* `unreadUrl` - урл для загрузки счётчика непрочитанных сообщений. По умолчанию: `https://backend.messenger.yandex.ru/unread_count`

Дефолты для блока с модификатором `_internal`:

* `loaderUrl` - iframe-загрузчик. По умолчанию: `https://gcn.yandex-team.ru/iframe-loader/stable/index.min.js`,
* `iframeUrl` - урл iframe мессенджера. По умолчанию: `https://q.yandex-team.ru/embed/`
* `unreadUrl` - урл для загрузки счётчика непрочитанных сообщений. По умолчанию: `https://backend.messenger.yandex-team.ru/unread_count`

### Подключение
* подключить блок `messenger`. Код блока лежит в [Лего-контрибах](https://github.yandex-team.ru/lego/islands/tree/dev/contribs/messenger) и релизится независимо от `islands` как npm-модуль `@yandex-lego/messenger`. Нужно сделать `npm i -S @yandex-lego/messenger --registry=http://npm.yandex-team.ru` и добавить уровни в enb-конфиг:
```
{path: 'node_modules/@yandex-lego/messenger/common.blocks', check: false},
{path: 'node_modules/@yandex-lego/messenger/deskpad.blocks', check: false},
```

### Использование тестового окружения (тестовый паспорт)
Необходимо установить параметры для блока `messenger`.

Для внешнего Q:
`iframeUrl: 'https://chat-dev-rr-templates.hamster.yandex.ru/chat?build=chamb&config=testing',`

`unreadUrl: 'https://backend.messenger.test.yandex.ru/unread_count',`

Для внутреннего Q:
`iframeUrl: 'https://messenger.test.yandex-team.ru/embed/?fetch=0',`

`unreadUrl: 'https://backend.messenger.test.yandex-team.ru/unread_count',`


### Использование альфа-окружения для тестирования (прод. паспорт)
Необходимо установить параметры для блока `messenger`.

Для внешнего Q:
`iframeUrl: 'https://chat-dev-rr-templates.hamster.yandex.ru/chat?build=chamb&config=development',`

`unreadUrl: 'https://backend.messenger.alpha.yandex.ru/unread_count',`

Для внутреннего Q:
`iframeUrl: 'https://messenger.alpha.yandex-team.ru/embed/?fetch=0',`

`unreadUrl: 'https://backend.messenger.alpha.yandex-team.ru/unread_count',`

### Сборка примеров
Для i-bem:
```
rm -rf .enb/tmp desktop.examples touch-phone.examples && npx bem make desktop.examples/messenger && npx bem make touch-phone.examples/messenger
```

Для React:
```
REACT_BLOCK=messenger npm run react-hot-examples
```

### Выпуск новой версии
- Увеличить версию в `./contribs/messenger/package.json`.
- Добавить описание изменений в `./contribs/messenger/CHANGELOG.md`.
- Создать файл с номером задачи в папке ` releases/notes/ISL-NNN.md`.
- Собрать и опубликовать версию.

### Сборка и публикация пакета
Получить права на публикацию во внутреннем npm можно у ответственных за пакет. Их список можно посмотреть командой:

```
cd ./contribs/messenger
npm show --registry=https://npm.yandex-team.ru
```

После чего выполнить сборку и публикацию пакета:

```
npm run react-messenger # сборка

cd ./contribs/messenger
npm publish --registry=https://npm.yandex-team.ru # публикация
```
