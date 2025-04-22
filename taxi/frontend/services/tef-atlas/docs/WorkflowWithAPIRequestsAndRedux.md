Реализация принятой в проекте логики запросов к серверу.

Функция **_makeRequest_** реализует вызов редакс экшенов при выполнении запроса к серверу:

1. перед запросом к серверу вызывает экшен с окончанием **Pending** в имени экшена
2. при успешном ответе вызывает экшен с окончанием **Success** в имени экшена
2. при ответе сервера с ошибкой вызывает экшен с окончанием **Failed** в имени экшена

пример использования 
```javascript

import {makeRequest} from 'utils/flow';

// стандартные экшены принятые в проекте для процесса запроса с сервера
const actions = { // (*) 
	anyActionPending: createAction('ANY_ACTION_PENDING'),
	anyActionSuccess: createAction('ANY_ACTION_SUCCESS'),
	anyActionFailed: createAction('ANY_ACTION_FAILED'),
}

const request = () => api.get('someEndpoint');

makeRequest(actions, request);
```

подразумевается что все необходимые операции с **response** сервера будут осуществляться в **then** от **request**.

### Генерация экшенов
Также были добавлены дополнительные функции для генерации экшенов вида (*)

```generateBaseActions(categiryPrefix, baseActionName)```

Ожидается, что **categiryPrefix** и **baseActionName** будут в UPPERCASE, как принято в проекте

```javascript
import {generateBaseActions} from 'utils/flow';

const actions = generateBaseActions('TAXIMAP', 'GET_HEATMAP_PARAMS');
```
на выходе получаем 
```javascript
generateBaseActions('TAXIMAP', 'GET_HEATMAP_PARAMS') === {
	getHeatmapParamsPending: createAction('TAXIMAP/GET_HEATMAP_PARAMS_PENDING'),
	getHeatmapParamsSuccess: createAction('TAXIMAP/GET_HEATMAP_PARAMS_SUCCESS'),
	getHeatmapParamsFailed: createAction('TAXIMAP/GET_HEATMAP_PARAMS_FAILED')
}
```
т.е. могут использоваться как обычно,
```javascript
dispatch(actions.getHeatmapParamsPending())
```

### Генерация редюсеров
Появилась возможность сгенерировать редьюсеры для таких экшенов, участвующих в загрузке данных с сервера, общий вид редьюсера применяемый в проекте
```javascript
const defaultState = {
	items: {
		data: [],
		status: null,
		desc: null
	}
}

const reducer = handleActions({
    [actions.getItemsPending]: (state, action) => { // action.payload вида {data, desc}
        return {
            ...state,
            items: {
            	...action.payload,
                status: 'pending'
            }
        };
    },
    [actions.getItemsSuccess]: (state, action) => {
        return {
            ...state,
            items: {
            	...action.payload,
                status: 'success'
            }
        };
    },
    [actions.getItemsFailed]: (state, action) => {
        return {
            ...state,
            items: {
            	...action.payload,
                status: 'failed'
            }
        };
    }
}, defaultState);
```
такой же редьюсер можно получить так
```javascript
import {generateBaseActions, getReducer} from 'utils/flow';

const actions = generateBaseActions('MY_PAGE_NAME', 'GET_ITEMS');
const reducer = getReducer([{actions, fieldName: 'items'}]) // где fieldName это ключ, верхнего объекта в state, вида {status, desc, data}
```