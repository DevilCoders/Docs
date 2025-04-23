###registerFeature

Этот хэлпер позволяет создавать самодостаточные фичи, которые могут быть переиспользваны целиком.

#### Пример использования:
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
```
#####Описание api:
- ```key``` ключ, с помощью которого фича будет добавлена в роутинг,
также используется как идентификатор страницы в коконе и в эпиках для определения,
что мы находимся на нужной странице (странице фичи).
- ```epics``` массив эпиков, которые нужны для работы фичи.
(При подключении фичи, эпики подключаются в порядке следования. Из-за этого эпики,
которые диспатчат экшены и на которые реагируют более общие эпики, лучше ставить последними)
- ```fulfilledSelector``` Селектор, который возвращает true, когда страница получила все
необходимые данные и ее можно отрисовать на клиенте/отдать с сервера.
- ```serverFulfilledSelector``` Необязательный параметр. Если он задан, то используется для определения
готовности страницы к отдаче с сервера. Обычно более строгий, чем fulfilledSelector.
Разделение нужно, если хочется на клиенте отрисовать страницу пораньше и всякие второстепенные данные
догружать уже в фоне.
- ```reducer``` структура редюсеров, необходимых для работы фичи.
- ```api``` апи, необходимое для фичи.

Все сущности (эпики, редюсеры, api) могут быть уже подключены другими фичами, в этом случае добавятся только
те, которые еще не были подключены.
