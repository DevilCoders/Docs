# ApiaryLayer

Слой для синхронизации Apiary. Позволяет получить доступ к контейнеру (тому что возвращается из View, `HTMLElement`), данным (data, которую сформировал контроллер), а также сгененрированному html и параметрам http запроса.

## Методы слоя

### Constructor
`constructor()`

```js
const mirror = new Mirror(); // создать mirror
const apiaryLauer = new ApiaryLayer(); // создать apiary-слой
```
Или с помощью [хелпера](../helpers.md)

```js
mirror = await makeMirror({
    jest: { // это будет передано в конструктор
        testFilename: __filename,
        jestObject: jest,
    }
});
apiaryLayer = mirror.getLayer('apiary');
```

### mountWidget

```
mountWidget<TWidgetProps>(
    pathToWidget: string,
    props?: TWidgetProps | ()=>TWidgetProps
): Promise<MountWidgetResult>
```

Рендерит виджет и монтирует в JSDOM

- `pathToWidget` - путь к виджету
- `props?` - данные для виджета или функция для формирования данных

Возвращает:

- `html: string` - Разметка виджета
- `container: HTMLElement` - DOM-контейнер в который смонтирован виджет
- `http.status: Array<{code: number; lock: boolean}>`- список HTTP-статусов выставленные виджетов
- `http.headers: Array<{name: string; value: string}>` - список HTTP-заголовков выставленные виджетов
- `data: unknown` - данные, которые вернул контроллер виджета

**Формирование пропов**

Чаще всего, будете передавать в качестве пропов объект. Но иногда виджет может принимать промис в качестве пропов (или их части).
В таком случае, в качестве пропов можно предать prop-функцию, задача которой вернуть необхоидмые пропы:

```ts
apiaryLayer.mountWidget('./widget', () => {
    const someResolver = require('./path/to/resolve');
    return {
        foo: 123,
        bar: someResolver()
    }
});
```

Функцию выполнится на бекенд-процессе, а ее результат будет передан виджету в качестве пропов.

> Внутри функции можно использовать async/await.

Prop-функция работает так же как `runCode`/`mock` и тп, то есть ничего не знает про область видимости, в которой объявлена.
Но, если по каким-то причинам необходимо передать ей какой-то аргумент из текущей области видимости, то, как и в `runCode`, можно привязать аргументы в момент объявления, при помощи специального хелпера:

```ts
import {packFunction} from '@yandex-market/testament/mirror';
apiaryLayer.mountWidget(
    './widget',
    packFunction(
        (foo, bar) => ({
            fooValue: foo,
            barValue: bar,
            // ...some other async madness
        }),
        ['foo value', 'bar value'],
    ),
);
```
