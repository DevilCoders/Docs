# Разработка

## Запуск проекта
```bash
npm ci
npm run build
npm run public
```

## Как тестировать
EcomTAP (SPA) сейчас открывается по-умолчанию, поэтому достаточно перейти на любую страницу `ecomm`

## Hermione
Для написания hermione-тестов есть тестовый [магазин](https://yandex.ru/turbo?text=spideradio.github.io%2Fyandexturbocatalog%2F&morda=1&ecommerce_main_page_preview=1&page_type=main&exp_flags=turbo-app-any-ua%3D1).
Данные для этого магазина (фид и страницы) лежат на [внешнем github](https://github.com/spideradio/spideradio.github.io).
Если для тестирования в магазине не хватает товара/скидки/картинки/чего угодно, нужно дописать данные во внешний репозиторий.
Лучше именно добавлять новые данные, а не изменять существующие, так как часть тестов уже завязанны на текущие данные.

### Hermione в Storybook

Когда нужно написать hermione-тест на компонент вне контекста всей страницы, то имеет смысл создать для него `Component.story.tsx` с примером и использовать его в тесте.

Для разработки story есть два пути:
1. Запустить команду `npm run storybook:serve` и открыть собранную витрину компонентов. Туннель при этом не строится, поэтому если вы работаете в QYP, то просто добавьте порт `9001` к адресу своей машины, например: `http://tenorok-dev.sas.yp-c.yandex.net:9001`.
2. Запустить команду `npm run storybook:build:watch` и `npm run start` и открыть адрес, похожий на используемый для гермиона-тестов: `/.stories/` (не забудьте слешик в конце).

Перед запуском гермиона-теста на основе сторибука необходимо собрать статику сторибука: `npm run storybook:build`.

Для открытия страницы конкретной story нужно использовать хелпер `yaOpenEcomStory('component', 'default')` — чтобы определить, что именно нужно передать ему в параметрах, можно посмотреть в адресную строку браузера во время выделения искомой story, например: `?path=/story/component--default`.

Как и в обычном гермиона-тесте, необходимо положить рядом testpalm.yml-файл, но так как данный сценарий не смогут выполнить асессоры, необходимо добавить тег `no_assessors`.

## CGI-параметры
1. `exp_flags=turbo-app-any-ua` — принудительный запуск tap без юзерагента супераппа
1. `exp_flags=turbo-app-test-preset` — возможности для тестирования:
    - `local` включает хождение за корзиной в темплар
    - `global` или `1` или `''` включает хождение за корзиной в тестовый бекенд и добавляет uid и oauth для проверки нативной оплаты
1. `&exp_flags=validate_counters=1` — флаг инициализации компонента `BaobabInjectorButton` для тестирования баобаба
1. `&frameDebug=1` — вывод в консоль всех исходящих postMessage и всех входящих, для которых есть обработчики
1. `&exp_flags=analytics-disabled=0&_ym_debug=1` — выводит в консоль логи метрики
1. `&exp_flags=error_counter=0` — отключить логирование ошибок

## SRCRWR
нужно не забыть добавить SAAS srcrwr для хождения в беты пулркевестов или хамстер `&srcrwr=SAAS%3ASAAS_ANSWERS`

## Тестирование на девайсах
- можно тестировать на бете ябро в андроид, не настраивая ничего дополнительно
- можно тестировать на девайсах, добавив манифест в chrome://turboapp-internals

### Набор для тестовой среды
- &srcrwr=SAAS%3ASAAS_ANSWERS&exp_flags=turbo-app-any-ua%3D1&exp_flags=turbo-app-test-preset

### Тестирование оплат
Тестирование работы с фреймом оплат можно производить на тестовом магазине ymturbo.t-dir.com
со следующими эксп-флагами: ?exp_flags=turbo-app-test-preset%3Dglobal&srcrwr=TURBO_HOST_CACHER%3ASAAS_KV_PRESTABLE

Пример ссылки:
https://yandex.ru/turbo/ymturbo.t-dir.com/n/yandexturbocatalog/?exp_flags=turbo-app-test-preset%3Dglobal&srcrwr=TURBO_HOST_CACHER%3ASAAS_KV_PRESTABLE

## Baobab
Blockstat и redir счетчики

### Как работать с баобабом
1. Обернуть основной комопонент Application HOC-ом withBaobabRoot (./utils/baobab/withBaobabRoot.tsx);
2. Обернуть каждую новую страницу проекта HOC-ом withBaobabPage (./utils/baobab/withBaobabPage.tsx);
3. Обернуть каждый компонент логирования HOC-ом wihtBaobab (@yandex-int/react-baobab-logger);

### withBaobabRoot
HOC withBaobabRoot предназначен для оборачивания основного компонента приложения (Application).
withBaobabRoot:
 - принимает основные параметры
 - строит вложенное баобаб дерево
 - отправляет дерево на сервер

### withBaobabPage
HOC withBaobabPage предназначен для оборачивания скринов-страниц приложения.


### Пример
```js
import { App } from './App';
import { withBaobabRoot } from './withBaobabRoot';
import { getBaobabParams } from './getBaobabParams';

const baobabParams = getBaobabParams(data, Util);
const AppWithBaobab = withBaobabRoot(baobabParams.rootAttrs, App);

React.hydrate(
    <AppWithBaobab baobab={baobabParams.params}>
)
```

## Эксперименты
[Небольшая дока](./experiments/README.md) о том, как можно заводить эксперименты.

## Турбо в СЕРПЕ
https://github.yandex-team.ru/serp/web4/blob/dev/src/vendors/turbo/README.md
