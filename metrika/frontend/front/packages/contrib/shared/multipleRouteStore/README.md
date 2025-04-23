UI компоненты Provider и Switch лежат в [@metrika/ui/components/MultipleRouteStore](../../ui/components/MultipleRouteStore)

Серверная часть находится в [@metrika/server/middlewares/render](../../server/middlewares/render)

# MultipleRouteStore

Штука объединяющая redux и react-router с поддержкой SSR.

Отвечает за создание стора и их смену при переходе между страницами.

## Принцип работы

Утилита работает с массивом страниц. У каждой страницы должен быть id, storeConfigurator и path (за исключением no-match страницы). Так же опционально можно указать init, forceReload и transfer (только клиент). Так же возможна более сложная настройка с использованием paramConfig (см. ниже)

При первом заходе на страницу выполняется цепочка действий. Сперва сопоставляется текущий pathname с массивом страницы - находится первое соответствие. Потом вызывается storeConfigurator с начальным состоянием, который создает наш стор для текущей страницы. Затем (при наличии) вызывается метод init, который запускает инициализирующие действия.

При переходе между страницами к данной цепочке добавляется действие. Перед вызовом storeConfigurator из старого состояние достается состояние уток входящих в массив transfer, описанный у новой страницы. Эти состояние передается как начальное состояние в storeConfigurator.

Подробное описание каждого параметра страницы:

* storeConfigurator -  функция отвечающая за создание стора. Ожидает увидеть в результате помимо самого стора метод dispose, поэтому лучше всего использовать вместе с reducktor. В качестве аргументов передается начальное состояние и history.

* init - функция отвечающая за запуск начальных экшенов. В качестве аргумента принимает store и expess request (на сервере).

* transfer - отвечает за перенос данных между сторами. Представляет из себя набор уток. Перекидывает состояние между утками с одинаковыми ключами.

* forceReload - говорит о том нужно ли обязательно пересоздавать стор, даже если они одинаковы (по умолчанию не пересоздает стор при одинаковой ссылке на storeConfigurator)

* paramConfig - нужен для того, чтобы разделить конфигурация страницы в зависимости от значения параметра урла. То есть, если path указан /path/:param, то его можно указать отдельную конфигурацию для каждого значения param.

    * paramName - говорит о том, по какому параметру мы хотим разделить конфигурацию
    * router - объект, где ключ - это значение параметр урла, а значение - это объект (storeConfigurator, init, transfer). Существует отдельный ключ _default, на который ссылаются все неизвестные параметры урла.

## SSR

Эта схема похоже работает и на сервере, но с несколькими особенностями.

* transfer не работает на сервере

* Нужно сообщить об окончании формирования стора, чтобы началась отрисовка страницы. Для этого существует утка initedDuck, когда стор полностью готов, достаточно вызвать action initedDuck.actions.init

## Best Practices

Лучше всего использовать вместе с router из [@metrika/shared/router](../router)

## Пример

```
const router = createRouter([
    { id: 'first', path: '/first' },
    { id: 'second', path: '/second/:param' },
]);

const multipleStoreRouter = router.extend<StoreProps>({
    first: {
        storeConfigurator: (state) => createStoreFromDucks(ducks, { state }),
        init: (store, request) => {
            store.dispatch(ducks.userDuck.actions.initial(request.user));
            store.dispatch(initedDuck.actions.init());
        },
        transfer: [ducks.userDuck],
    },
    second: {
        paramConfig: {
            paramName: 'param',
            router: {
                _default: {
                    storeConfigurator: (state) => createStoreFromDucks(ducks, { state }),
                    init: (store) => store.dispatch(initedDuck.actions.init()),
                    transfer: [ducks.userDuck],
                },
            },
        },
    }
})

const routes = multipleStoreRouter.get();

<Provider routes={routes} state={state}>
```