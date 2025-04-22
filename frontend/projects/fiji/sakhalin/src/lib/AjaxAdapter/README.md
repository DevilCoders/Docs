# AjaxAdapter

Существует 2 варианта работы с react адаптерами посредством ajax-запросов:
1) Загрузка дополнительных данных из уже добавленной на страницу react фичи;
2) Загрузка отрендеренной на сервере react фичи и добавление её в контейнер на странице.

Рассмотрим подробнее оба варианта.

## 1. Загрузка дополнительных данных

По умолчанию любой адаптер будет отвечать на ajax-запросы пустым ответом. Для того чтобы переопределить такое поведение нужно в адаптере фичи реализовать метод `ajax`.

Допустим, у нас есть адаптер `AdapterSomeFeature` и мы хотим, чтобы при клике на кнопку, в фиче что-то обновилось.

1. Опишем интерфейсы входных и выходных параметров для метода ajax:

```ts
interface IAjaxParams {
    // ... входные параметры метода ajax
}

interface IAjaxResponse {
    // ... выходные параметры метода ajax
}
```

2. Реализуем в адаптере метод `ajax`:

```ts
export class AdapterSomeFeature extends Adapter<ISnippet> {
    ajax(params: IAjaxParams): IAjaxResponse {
        return this.getSomething();
    }

    // ...
}
```

Теперь на ajax-запросы адаптер `AdapterSomeFeature` будет отвечать данными, необходимыми для обновления фичи на клиенте.

3. Следующим шагом нужно добавить нашему блоку возможность обрабатывать ajax-запросы.

Вся работа по подгрузке данных посредством ajax-запросов из реактовых фичей происходит через специальный блок `i-react-ajax-adapter`. Для добавления его на страницу нужно подготовить бандлы вызовом функции `setupAjaxAdapter` внутри метода `render()`.

```ts
import { setupAjaxAdapter } from 'sakhalin/src/lib/AjaxAdapter/setup';

export class AdapterSomeFeature extends Adapter<ISnippet> {
    // ... ранее описанный метод ajax

    render() {
        setupAjaxAdapter(this.context);

        // ...
    }
}
```

4. Теперь в компоненте с фичёй можно сделать ajax-запрос к адаптеру с помощью метода `ajaxRequest`:

```ts
import { ajaxRequest } from 'sakhalin/src/lib/AjaxAdapter';

export const SomeFeature = () => {
    const [something, setSomething] = useState();

    const loadSomething = useCallback(() => {
        ajaxRequest<IAjaxParams, IAjaxResponse>({
            type: 'SomeFeature',
            adapterParams: {
                // ... параметры в формате IAjaxParams
            }
        }).then(
            response => setSomething(response),
            error => console.log(error)
        );
    }, []);

    return (
        /* ... */
        <button onClick={loadSomething}>
            Загрузить дополнительные данные
        </button>
        /* ... */
    );
};
```

## 2. Загрузка React фичей

### Загрузка из реакт кода

Для полной перезагрузки фичи из реакт кода можно воспользоваться метод `ajaxRender`:

```ts
import { ajaxRender } from 'sakhalin/src/lib/AjaxAdapter';

export const SomeFeature = () => {
    const container = useRef(null); // Создаём ref для контейнера, куда будет рендериться фича

    const loadFeature = useCallback(() => {
        ajaxRender<IAjaxParams>(container.current, {
            type: 'SomeFeature',
            adapterParams: {
                // ... параметры в формате IAjaxParams
            }
        });
    }, []);

    return (
        <>
            <div ref={container}>

            <button onClick={loadFeature}>
                Загрузить фичу
            </button>
        </>
    );
};
```

### Загрузка из i-bem кода

Иногда возникает необходимость подгружать react фичи отложенно из i-bem кода, например догружать react фичу, скрытую за кликом.

1. Реализовать адаптер, который будет рендерить фичу.

```ts
export class AdapterSomeFeature extends Adapter<ISnippet> {
    render() {
        return <App />;
    }
}
```

2. Реализовать i-bem блок-загрузчик, в котором нужно добавить загрузчик React фичей:

```js
blocks['some-feature-loader'] = function(data) {
    blocks['i-react-ajax-adapter'](data); // добавляем на страницу загрузчик react фичей

    return {
        block: 'some-feature-loader',
        js: true
    };
};
```

3. В клиентской реализации блока-загрузчика вызвать загрузку React:

```js
BEM.DOM.decl('some-feature-loader', {
    onSetMod: {
        js: {
            inited: function() {
                BEM.channel('i-react-ajax-adapter').trigger('render', {
                    container: this.domElem,
                    params: { type: 'SomeFeature' },
                    callback: function(error) {
                        // Тут можно добавить логику, которая выполнится после загрузки фичи или обработать ошибку
                    }
                });
            }
        }
    }
})
```

4. Фича на реакте загружена и готова к работе. Также можно взаимодействовать с реактом из i-bem через [специальную шину reactBus](../../components/ReactBus/README.md).
