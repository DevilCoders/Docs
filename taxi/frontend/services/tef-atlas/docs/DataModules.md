Появились случаи, когда нужно использовать одну и ту же часть кода работы с данными в нескольких контейнерах.  
Для того, чтобы переиспользовать набор api, reducer, selectors, были реализованы DataModules.

Суть в том, что мы в одном месте описываем всю логику получения и обработки данных и независимо используем её в разных контейнерах одновременно.

### Объявление DataModule
```javascript
import dataModule from 'utils/DataModule/DataModule';
const MyDataModule = dataModule({
    defaultState: {...}, // стейт по умолчанию
    reducer: {
        actionName: (state, action) => {...} // action будет создан автоматически
    },
    selectors: myModule => ({ // В функцию прилетит экземпляр модуля
        getSomeData: createSelector(
            myModule.selectors.moduleData, // Селектор, который вернёт объект состояния модуля
            moduleData => moduleData.some.nesting.staff
        )
    }),
    api: ({actions}) => ({ // У экземпляра модуля есть сгенерированный объект actions
        loadData: () => (dispatch, getState) => {
           dispatch(actions.actionName())
        }
    }),
    otherStuffAsAnything: {...}, // Можно объявить любые свойства
    otherStuffAsFunction: myModule => {} // Если объявить свойство как функцию, в неё прилетит экземпляр модуля
});

```
### Создание экземпляра модуля
```javascript
const myDataModule = MyDataModule(
    'taximap.myDataModule', //Обязательно нужно передать путь редюсера
     'ACTIONS/SUBPATH' // А вот Actions subpath передавать необязательно. По умолчанию это путь редюсера
);

// На выходе получаем следующее
console.log(myDataModule);
// ->
{
    defaultState,
    reducer,
    actions,
    selectors: {moduleData, getSomeData},
    api,
    reducerPath,
    actionsSubpath,
    otherStuffAsAnything, // будет передано ровно то, что объявили в модуле
    otherStuffAsFunction // будет передано то, что вернула функция, объявленная в модуле
}
```

### Плагины
Обратите внимание на вышеописанный `otherStuffAsFunction`.  
Если в объявлении модуля передать функцию, в момент создания экземпляра модуля, в эту функцию будет передан экземпляр модуля. Таким образом, мы можем писать плагины.

К примеру, мы можем написать плагин, который добавит в reducer новые свойства и экшены.
```javascript
const myPlugin = () => module => {
    module.defaultState = {
        ...module.defaultState,
        myPluginParam: null
    }

    const action = createAction(`${module.actionsSubpath}/myPluginAction`);
    const actionHandler = (state, action) => ({...state, myPluginParam: action.payload})

    module.actions = {
        ...module.actions,
        myPluginAction: action
    }

    module.actionHandlers = {
        ...module.actionHandlers,
        [action]: actionHandler
    }
}

// Используем плагин в объявлении модуля
const MyDataModule = dataModule({
    myPlugin: myPlugin()
})
```

### Плагин запросов
Чтобы можно было использовать [принятую в проекте логику запросов к серверу](WorkflowWithAPIRequestsAndRedux.md) в датамодулях, был реализован плагин запросов.

Суть плагина проста. Мы хотим описать запрос, но не хотим описывать reducer-ы, action-ы и прочую логику, которая проставит статус запроса и положит данные запроса в store.  
Мы просто хотим использовать функцию, которая сделает запрос и сразу работать с данными по запросу из redux-а.

**Пример использования**
```JavaScript
// PLUGIN FILE somepath/requests.js
import {requestPlugin} from 'utils/DataModule/DataModule';

export default requestPlugin({
    loaders: {
        /**
         * module - собственно инстанс модуля, со всеми экшенами, селекторами и т.д..
         * requestPayload - параметры запроса (всё что угодно).
         **/
        get: (module, requestPayload) => HttpApi.post('some/url')
    },
    entity: 'someEntityName' // Опционально - название сущности. 
                             // Если присутствует, то редюсер углубится на 1 уровень с ключем entity. 
                             // Иначе requestPlugin раскатает state лоадера прям в корень модуля.
});

// DATAMODULE FILE somepath/myModule.js
import dataModule from 'utils/DataModule/DataModule';
import requests from './requests';

export default dataModule({
    requests
});
```

В результате, в defaultState модуля, плагин добавит следующие свойства
```javascript
{
    someEntityName: {
        requestData: null, // Параметры последнего запроса
        data: null, // данные, полученные в результате запроса
        status: null, // статус запроса - pending, success, failed
        desc: null // данные об ошибке, в случае status = failed
    }
}
```

Все экшены (для pending, success, fail, reset) плагина будут доступны в module.actions и их можно использовать.  
Функция для запроса также будет доступна в модуле.  
Например из api:  
```JavaScript
// API FILE somepath/api.js
export default module => ({
    loadSomething: (params) => dispatch => {
        const {requests} = module;

        return requests.get(params);
    }
});

// DATAMODULE FILE somepath/myModule.js

import dataModule from 'utils/DataModule/DataModule';
import requests from './requests';
import api from './api';

export default dataModule({
    api,
    requests // называть здесь параметр requests совсем необязательно. Может быть любой другой ключ
});
```

### Реальные примеры в коде
Все описанные датамодули лежат в папке `/static/dataModules`.  
Как используется плагин запросов можно посмотреть в модуле DriverTrack
* [Объявление плагина и описание запроса](https://a.yandex-team.ru/arc_vcs/taxi/frontend/services/tef-atlas/src/dataModules/DriverTrack/requests.js)
* [Подключение плагина в датамодуль](https://a.yandex-team.ru/arc_vcs/taxi/frontend/services/tef-atlas/src/dataModules/DriverTrack/DriverTrack.js)
* [Использование запроса в api](https://a.yandex-team.ru/arc_vcs/taxi/frontend/services/tef-atlas/src/dataModules/DriverTrack/api.js)

[Описание редюсеров в ручном режиме](https://a.yandex-team.ru/arc_vcs/taxi/frontend/services/tef-atlas/src/dataModules/GraphAdjustment/reducer.js) можно посмотреть в модуле GraphAdjustment
