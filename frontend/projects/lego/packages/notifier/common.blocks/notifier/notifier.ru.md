# notifier

`notifier` – обёртка над [Центром уведомлений](https://a.yandex-team.ru/arc_vcs/frontend/services/gnc-frame).

### Требования
Компонент в технологии `react` использует `fetch` и `Promise`, для корректной работы в старых браузерах необходимо использовать `polyfill`:
* `fetch` — [whatwg-fetch](https://www.npmjs.com/package/whatwg-fetch)
* `Promise` — [es6-promise](https://www.npmjs.com/package/es6-promise)

### Состав
* `__icon` – иконка
* `__popup` — `popup2`, в него кладётся iframe с ЦУ
* `__ticker` — счётчик непрочитанных, можно задать через `bemjson`. Обновляется через RPC-канал методом `onUpdateCounter`.
* `_polling_yes / polling (React)` – модификатор, который позволяет обновлять колокольчик (и включать красную точку, если получены новые сообщения). Стандартно раз в 30 секунд. Регулируется через параметр `pollInterval`.

### Принцип
При инициализации блок подключает [скрипт-загрузчик(Atom)](https://a.yandex-team.ru/arc_vcs/frontend/projects/lego/packages/iframe-loader), вставляет в попап iframe с ЦУ и `spin2` заменяется ЦУ.

#### Как инициализируется ЦУ:
При инициализации `notifier` грузится скрипт `iframe-loader`, который грузит страницу `/gnc/frame` и вызывает `onIframeLoad` в `notifier` после загрузки iframe.

### JS-параметры
* `loaderUrl` – путь до скрипта загрузчика [скрипт-загрузчик(Atom)](https://a.yandex-team.ru/arc_vcs/frontend/projects/lego/packages/iframe-loader). По-умолчанию `https://yastatic.net/s3/frontend/iframe-loader/v0.1.1/index.min.js`
* `iframeUrl` – путь до `HTML` виджета. Скорее всего вам нужна стабильная версия - `https://yandex.TLD/gnc/frame`.

* `apiHost` – URL для похода в базу данных. Для тестирования внутренних сервисов можно использовать `http://api-stable.dst.yandex-team.ru/tracker/`.
* `counterHandle` – URL для похода за чтения тикера. По умоланию: `https://yandex.TLD/bell/api/v1/get-ticker` для внешней сети, `https://bell.yandex-team.TLD/bell/api/v1/get-ticker` для внутренней сети.

### JS-параметры, которые больше не используются
* `lang` – язык Центра уведомлений устанавливается автоматически.
* `domain` –  домен верхнего уровня, на котором будет работать Центр уведомлений, совпадает с доменом в `iframeUrl`.
* `source` – идентификатор сервиса (для метрики). Например, `tracker`.
* `serviceDatabaseId` – id корневой базы данных, в которой хранится вся основная информация. Например, для внутренних сервисов `serviceDatabaseId` это `.pub.notifier@notification_services`.
* `services` – массив строк из названий сервисов для фильтрации уведомлений по коллекциям. По умолчанию не задан, уведомления показываются от любого сервиса (из любой коллекции).
* `counterParams` – параметры для счетчиков центра нотификаций
* `referrer` – параметр который будет использоваться в качестве actionURL для счетчиков центра нотификаций


### Подключение
* получить от бэкенда `apiHost` и `serviceDatabaseId`
* подключить блок `notifier`. Код блока лежит в [Аркадии](https://a.yandex-team.ru/arc_vcs/frontend/projects/lego/packages/notifier) и релизится как npm-модуль `@yandex-lego/notifier`. Нужно сделать `npm i -S @yandex-lego/notifier --registry=http://npm.yandex-team.ru` и добавить уровни в enb-конфиг:
```
{path: 'node_modules/@yandex-lego/notifier/common.blocks', check: false},
{path: 'node_modules/@yandex-lego/notifier/deskpad.blocks', check: false},
```

Внутренние сервисы могут использовать блок `m-head`. Ему нужно передать JS-параметры:
```
{
    block: 'm-head',
    // ...
    notifier: {
        apiHost: 'https://cloud-api.yandex-team.ru/tracker/',
        lang: 'uk',
        source: 'lego',
        serviceDatabaseId: '.pub.notifier@notification_services_yateam', // внутренние сервисы
        domain: 'ru'
    }
}
```
