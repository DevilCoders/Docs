# analytics

##### Перед началом разработки:

Нужно настроить деплой серверного бандла.
Самый простой способ - создать в папке ```./isomorphic``` файл ```.deploy.json```
с содержимым вида:
```json
{
  "root": "/home/${userName}/node.partner.market_${userName}",
  "host": "market.logrus01hd.yandex.ru",
  "port": 22,
  "username": "userName",
  "privateKey": "/Users/${userName}/.ssh/id_rsa",
  "passphrase": "passphrase"
}
```

Или настроить синхронизацию папки ```./lib``` с логрусом через rsync или другими способами.

##### Начало разработки:

- Запуск на логрусе (статика будет загружаться с логруса) ```npm run isomorphic:server```
- Запуск на логрусе (статика будет загружаться с localhost) ```npm run isomorphic:dev-server```
- Запуск сборки клиента и сервера на ноуте ```npm run analytics:build:watch```

Если не нужно добавлять новые резолверы на сервер и нужно просто поверстать,
на ноуте можно просто запустить ```npm run analytics:build-client:watch```.
После сборки клиента запустить один раз ```npm run analytics:build-server```.

Это нужно, чтобы собрать сервер, который будет знать о локально собранном
клиенте и о необходимых для подключения чанках.

##### Добавление новых страниц

Каждая страница в аналитической платформе - это компонент, который загружается динамически
и выносится в отдельный бандл. Также каждая страница должна быть самодостаточна и должна
самостоятельно подключать необходимые зависимости.

Ожидание и подключение страниц реализовано в [registerFeature](https://github.yandex-team.ru/market/partnernode/isomorphic/helpers/registerFeature/README.md)

###### Пример:
- Создать папку в ```./analytics/containers``` например ```./analytics/containers/Search```
- Создать файл ```index.js``` он подключает необходимые зависимости и экспортирует корневой
компонент страницы
```js
// @flow

import {registerFeature} from 'isomorphic/helpers/registerFeature';
import myEpic from 'analytics/containers/App/epics/collections/myEpic';
import {myReducer} from 'analytics/containers/App/reducers/collections/myReducer';
import myApi from 'analytics/containers/App/api/myApi';

import epic from './epics';
import {myWidget} from './reducers';
import {key} from './constants';
import MyComponent from './components';
import {myFulfilledSelector} from './selectors';

const withFeature = registerFeature({
    key,
    epics: [myEpic, epic],
    fulfilledSelector: myFulfilledSelector,
    reducer: {
        widgets: {
            myWidget,
        },
        collections: {
            myReducer,
        },
    },
    api: {
        myApi,
    },
});

export default withFeature(MyComponent);
```
[Более подробно про registerFeature](https://github.yandex-team.ru/market/partnernode/isomorphic/helpers/registerFeature/README.md)
- Добавить страницу в роутинг ```./analytics/routes/index.js```
```js
import {key as search} from 'analytics/containers/Search/constants';

const routes = {
    [search]: {
        // путь, на котором нужно отрисовать компонент,
        // может быть как строкой, так и массивом строк ('/path-a' или ['/path-a', '/path-b'])
        path: searchPath,
        // нужно ли ходить в кокон за правами к странице
        checkAccess: true,
        // должен ли url полностью матчится на текущий path или только начинаться с него
        exact: true,
        // компонент страницы, отрисовывающийся на роуте
        // обязательно должен быть завернут в динамический импорт и loadable
        component: loadable(() => import('analytics/containers/Search')),
    },
}
```
- Добавить роут туда, где он должен отрисоваться, например в ```./analytics/containers/Layout```
```js
import {key as search} from 'analytics/containers/Search/constants';

const routeNames = [search];

const Layout = () => (
    <div className={cx(css.root)}>
        <Header />
        <main className={cx(css.main)}>
            <AppRoutes routeNames={routeNames} />
        </main>
        <Footer />
    </div>
);
```

Связка этого всего идет через ключ из ```analytics/containers/Search/constants```
```js
// @flow

export const key = 'market-analytics-platform:page:search';
export default key;
```

Он также используется как идентификатор страницы в коконе и с его помощью в эпиках можно определить,
что мы находимся на нужной странице и нужно выполнять определенные действия (например, загружать данные, необходимые на странице)

##### Работа с локализацией:
Локализация аналитическй платформы заводится в [танкере](https://tanker.yandex-team.ru/?project=analyticsPlatform&branch=master)
После этого выгружается в [бункер](https://bunker.yandex-team.ru/analyticsplatform/tanker).
Если возникают проблемы с этими сервисами и невозможно получить актуальную локализацию,
в репозиторий выгружается файл с локализациями для фолбэка. Делается это командой ```npm run analytics:i18n``` 
