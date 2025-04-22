# Турбо-приложение для Такси и Доставки

[Wiki о проекте с общей информацией](https://wiki.yandex-team.ru/taxi/frontend/turboapp-taksi/)

Ссылки:
- [Графики балансера – тестинг](https://yasm.yandex-team.ru/template/panel/tap/upstream=taxi-testing-total/)
- [Графики балансера – продакшн](https://yasm.yandex-team.ru/template/panel/tap/upstream=taxi-total/)

Приложение "Доставка" по кодовой базе ничем не отличается от "Такси". Разница лишь в доступных тарифах.

## Запуск

Устанавливаем зависимости:
```bash
npx lerna bootstrap --scope @yandex-int/turboapp-taxi --include-filtered-dependencies
```

Для локальной разработки приложения "Такси" запускаем скрипт:
Мобилки/Планшеты:
```bash
npx lerna run start --scope @yandex-int/turboapp-taxi --stream 
```

Десктопная версия:
```bash
npx lerna run start-desktop --scope @yandex-int/turboapp-taxi --stream
```

Для локальной разработки приложения "Доставка" запускаем скрипт:
```bash
npx lerna run start-delivery --scope @yandex-int/turboapp-taxi --stream
```

Открыть приложение можно через туннелер, ссылка формата `https://<username>-<project_id>-<inst_name>.ldev.yandex.ru` видна в консоли при запуске. Пример ссылки: `https://tapdeveloper-1-ekb.ldev.yandex.ru`.

Для работы авторизации и других запросов в десктопном браузере необходимо добавить подстроку `TA/2.1` в `User agent`.

Приложение автоматически перезапустится при изменениях в коде.
Ошибки линтинга можно увидеть в консоли.

## Команды

- `npm start` – запуск приложения в режиме разработки
- `npm run build` – сборка production версии приложения
- `npm run update-api-stub` – обновление моков для API

## Разработка

- [Подробнее про стор](./src/redux/README.md)
- Документация по [Create React App](https://facebook.github.io/create-react-app/docs/getting-started/).
- Документация по [React](https://reactjs.org/).

АПИ Такси доступно по двум путям:
- https://ya-authproxy.taxi.yandex.ru - Продовое окружение Такси.
- https://ya-authproxy.taxi.tst.yandex.ru - Тестовое окружение Такси.

Для наших продовых хостов ([taxi.tap.yandex.ru](https://taxi.tap.yandex.ru) и [taxi.tap-rc.yandex.ru](https://taxi.tap-rc.yandex.ru)) мы осуществляем походы в продовое окружение АПИ Такси. Во всех остальных случаях пользуемся тестовым окружением АПИ.

Мониторинг за состоянием бекенда такси для турбоапа:
* [График в Соломон](https://solomon.yandex-team.ru/?cluster=production&l.group=dorblu_rtc_taxi_api-proxy_*&l.host=cluster&l.object=api-proxy_taxi_yandex_net_integration_turboapp&project=taxi&l.sensor=ok_rps&service=dorblu&graph=auto)
* [Алерты](https://solomon.yandex-team.ru/admin/projects/taxi/alerts/3ef59d48-4cba-46e7-896c-5ab2e1fe36cb)
* [Канал в juggler](https://juggler.yandex-team.ru/raw_events/?query=host%3Dcluster%26service%3Dturboapp-rps-limiter)
* [Уведомления](https://juggler.yandex-team.ru/notification_rules/?query=rule_id=5e6a2f20dcc66c00719879e2)

## Тестирование

[Аккаунты для тестирования](https://yav.yandex-team.ru/secret/sec-01dzrjjdvkpy9f9tjh36y4gc39/)

В режиме отличном от production при заказе такси в Москве эмулируется поездка с фейковым водителем.
Через GET-параметр `comment` можно указать комментарий к заказу, позволяющий влиять на эмуляцию.
Так, например, можно уменьшить время ожидания, время прибытия и время в пути (`comment=search-10,wait-10,speed-1000`).
Подробнее про возможные [комментарии к заказу](https://wiki.yandex-team.ru/users/alexsandrl/comment/).

Релизные стенды доступны по двум путям:
- https://taxi.tap-rc.yandex.ru - Продовое АПИ Такси.
- https://taxi-test.tap-rc.yandex.ru - Тестовое АПИ Такси.

Тестовые стенды:
- https://taxi-pr-{id_pr}.tap-tst.yandex.ru/ - Мобилки
- https://taxi-desktop-pr-{id_pr}.tap-tst.yandex.ru/ - Десктоп

### Тестовая оплата

- [Тестовые карты для успешной оплаты](https://kassa.yandex.ru/developers/using-api/testing#test-bank-card-success)
- [Тестовые карты для проверки ошибок оплаты](https://kassa.yandex.ru/developers/using-api/testing#test-bank-card-cancellation-details)

## Молли

Каждый день запускается [таска в sandbox](https://sandbox.yandex-team.ru/scheduler/19604/view), которая
проверяет приложение на уязвимости (система "Молли": https://wiki.yandex-team.ru/product-security/molly).

## Мониторинг ошибок

-   [Проект в Error Booster](https://error.yandex-team.ru/projects/turboapp-taxi/projectDashboard)
-   [Ошибки в проде за последний час](https://error.yandex-team.ru/projects/turboapp-taxi/projectDashboard?filter=environment%20==%20production&period=hour)
-   [Конфиг алертов](https://error.yandex-team.ru/projects/turboapp-taxi/settings/alerts)
-   [Настройки уведомлений](https://juggler.yandex-team.ru/notification_rules/?query=namespace%3DTAP)

## Пакет с приложением

Содержимое файла `src/package.ts` также публикуется как пакет для вставки турбоаппа в веб-сервис Такси.

### Параметры
```typescript jsx
type TurboappOptions = {
    mode: TurboappTaxiMode;
    ym?: TurboappMetrika;
    errorLogger?: RumLogger;
    rum?: typeof Ya.Rum;
    fetchExperiments?: () => Promise<FlagMap>;
    yandexuid?: string;
    reqId?: string;
    settings?: SettingsType;
    features?: FeaturesType;
};
```
* `mode` — Режим работы сервиса: турбоапп или такси.
```typescript jsx
enum TurboappTaxiMode {
    Turboapp = 'turboapp',
    Taxi = 'taxi',
}
```
* `ym` — Функция для отправки событий в метрику
```typescript jsx
type TurboappMetrika = (method: string, ...args: unknown[]) => void;
```

* `errorLogger` — инициализированный логгер из `@yandex-int/error-counter`
* `rum` — инициализированный логгер из `@yandex-int/rum-counter`
* `fetchExperiments` — функция для загрузки значений экспериментов
* `yandexuid` — используется в дебаг-панели
* `reqId` — используется для идентификации запросов в бэкенд. Можно использовать uuid
```typescript jsx
declare const fetchExperiments: () => Promise<FlagMap>;

type FlagMap = Record<string, string | number | boolean>;
```

* `settings` — Произвольные настройки приложения.

```typescript jsx
import { ReactChild } from 'react';

enum PromoTypeMode {
  App = 'app',
  Driver = 'driver',
}

type SettingsType = {
  authorizationType: AuthorizationType.Phone | AuthorizationType.Startup, // Авторизация по телефону либо через стартап
  menuPromoType: PromoTypeMode.Driver, // Промо в мобильном меню
  renderMenuBanner: (params: RenderMenuBanner) => null | ReactChild, // Произвольный рендер баннера в меню
  withCallcenterPromo: false, // Нужно ли показывать промо КЦ
  withFooter: false, // Нужно ли показывать футер
  footerLinksBuilder: ({ zoneName }) => ([{ title: 'тарифы', url: '/tarriffs' }, { title: 'изменить язык', onClick: () => {}}])
  menuBuilder: ({ zoneName }) => ([[{ title: '', url: '' }]])
  disableCache: true, // Нужно ли отключить кэширование стора. (Нужно отключить для fleet кабинета)
  disableBindCard: false, // Выключить добавление карты
  trustHost: 'https://trust.yandex.ru', // Хост траста
  brand: 'yandex' | 'yango' | 'vezet', // копирайты/баннеры
  copyright: 'MLU', // копирайты/баннеры
  hideOrderPromo: false, // скрыть баннер в заказе
  apiOptions: {
    needNetworkMiddleware: true, // Нужна ли проверка интернета
    needCsrf: true, // Нужен ли csrf токен для похода в ручки
    host: 'https://api.fleet.tst.yandex.ru', // Основной хост апи
    prefix: '/fleet', // Префикс для всех ручек
    extraHeaders: {
      'X-Park-Id': 'c5cdea22ad6b4e4da8f3fdbd4bddc2e7',
    }, // Доп хедеры которые нужно слать в заказыы
    xTaxiService: '', // докидывает сервис в заголовок x-taxi
    passportHost: 'https://passport.yandex.ru', // для авторизации        
    userInfoUrl: '/user-info', // Адрес ручки юзера https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/turboapp-taxi/src/lib/auth/user-info.ts
    geolocationUrl: '/api/v1/geolocation', // Адрес ручки ip-геолокации
  },
  map: MapType.Google // Показывать гугл карту или яндекс карту по дефолтуы
};
```
### Использование пакета

```typescript jsx
import { createTurboappTaxi, TurboappTaxiProps } from '@yandex-int/turboapp-taxi';

const TurboappTaxi: React.FC<TurboappTaxiProps> = createTurboappTaxi({
    mode: TurboappTaxiMode.Turboapp,
    ym: (method: string, ...args) => ym(123, method, ...args),
    errorLogger: errorLogger,
    rum: window.Ya.Rum,
    experiments: () => Promise.resolve({ 'exp1': true }),
    reqId: uuid(),
    settings: {menuPromoType: 'driver'},
});

const App = () => <TurboappTaxi header={<AppHeader />} promo={<AppPromo />} footerElem={<Langdetect />}/>;
```

### Правила csp

Из пакета экспортируются правила csp, необходимые для работы компонента-приложения

```javascript
const turboappTaxiCsp = require('@yandex-int/turboapp-taxi/csp');

const turboappTaxiCspPresets = csp.presets(staticHost); // staticHost – хост, с которого раздается статика приложения
```

Полученные пресеты можно использовать в `express-yandex-csp`

### Работа с веб-пушами

Из пакета экспортируется функция, подписывающая service worker на обработку пуш-уведомлений

```typescript
import { enableWebPush } from '@yandex-int/turboapp-taxi/web-push';

enableWebPush(self);
```

### Полифиллы

Для работы компонента в старых браузерах необходимо подключить полифиллы
из пакета с помощью метода `applyPolyfills`.
Метод возвращает промис, выполнение которого нужно дождаться,
прежде чем отображать компонент


```typescript
import { applyPolyfills } from '@yandex-int/truboapp-taxi/polyfills';

applyPolyfills().then(() => {
    // рендер приложения
});
```

### Локализация

```typescript
import { loadI18N } from '@yandex-int/truboapp-taxi/lib/i18n';

loadI18N(LANG).then(() => {
  // рендер приложения
})
```

### Добавление переводов

Для добавления перевода, вначале нужно добавить ключ в [танкер турбоаппа](https://tanker-beta.yandex-team.ru/project/turboapp-taxi/keyset/common?branch=master)

Кнопка `Добавить ключи` -> Ввести название ключей и перевод -> Кнопка `Создать ключи`

После этого выполнить `tanker pull`, заменить текст в файле на `i18n('Название ключа')`

### Добавление нового языка

1) Добавить язык в [config.tanker.langs](.tanker/config.js)
2) Добавить мапинг в [TRANSLATIONS_MAP](./src/lib/i18n/index.ts)
3) Проверь, что новый язык [добавлен](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/i18n/src/plural) в пакет i18n 
4) `tanker pull -f`
5) Если не удается выполнить команду, то попробуй [добавить токен](https://wiki.yandex-team.ru/search-interfaces/tanker/tanker-kit/#oauth) под именем TANKER_TOKEN 

Если новый язык нужно добавить с без добавления новых переводов, то его можно смапить на уже имеющиеся в проекте, указав его код в [mapping](./src/lib/i18n/index.ts):
```
const mapping: {[x: string]: Language} = {
  // iw: 'he',
  nn: 'no',
  nb: 'no',
};
```

### Версии для desktop и mobile

По умолчанию экспортируется мобильная версия

```typescript jsx
import { createTurboappTaxi } from '@yandex-int/turboapp-taxi';
```

Чтобы явно подключить нужную версию, нужно импортировать следующим образом:

```typescript js
// Мобильная версия
import { createTurboappTaxi } from '@yandex-int/turboapp-taxi/TurboappTaxi/mobile';

// Десктоп версия
import { createTurboappTaxi } from '@yandex-int/turboapp-taxi/TurboappTaxi/desktop';
```

### Как создать водителя в тестинге и самому принять свой заказ
https://wiki.yandex-team.ru/users/zachesova/kak-sozdat-voditelja/

переходим по ссылке и выполняем все пункты.

Дальше устанавливаем себе таксометр отсюда https://teamcity.taxi.yandex-team.ru/buildConfiguration/DailyDevBuilder/5925970?buildTab=artifacts
