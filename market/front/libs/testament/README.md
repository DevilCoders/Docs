# Testament

Платорма для написания виджетных тестов (интеграционных тестов для виджетов) в Яндекс.Маркете

Виджетные тесты помогают проверить, что:

- генерируется верная разметка
- генерируются верный стейт
- виджет ожидаемо ведет себя на клинте

Виджет должен быть максимально изолирован - ресурсы должны быть замоканы.

## Цель проекта

1. Способствовать миграции E2E-тестов в виджетные. Это позволит покрывать интерфейс более быстрыми и стабильными
   тестами, **без внешних зависимостей**.
2. Унифицировать подходы к разработке виджетных тестов

## Быстрый старт

1. Добавьте в зависимости проекта `@yandex-market/testament`
2. Настройте jest

```
{
    testRunner: '@yandex-market/testament/runner',
    testEnvironment: '@yandex-market/testament/env',
    resolver: '@yandex-market/testament/resolver'
}
```

3. Монтируйте apiary-виджеты и тестируйте их поведение

## Концепция

Рендеринг виджета происходит в два этапа:

1. Серверный процессинг — виджет обрабатывается при помощи apiary processor, который запускает контроллер виджета и
   получает разметку
2. Клиентский рантайм - полученная разметка монтируется в JSDOM и выполняется применение apiary-патчей и гидрация
   react-компонента

Серверный процессинг выполняется в дочернем nodejs процессе (процессе рендеринга), поэтому необходимо убедиться в том,
что среды выполнения в jest-процессе и процессе ренедеринга - одинаковы.

Для этого testament предоставляет mirror - набор методов, позволяющих синхронизировать среды исполнения. Функционалность
которую хочется синхронизировать представлена в виде слоя (layer). Основная идея заключается в том, что вызывая метод в
основном процессе - он автоматически вызывается и в процессе рендеринга.

```ts
import Mirror from '@yandex-market/testament/mirror';
import JestLayer from '@yandex-market/testament/mirror/layers/jest';

const mirror = new Mirror(); // создать mirror
const jestLayer = new JestLayer(__filename, jest); // создать jest-слой

await mirror.registerLayer(jestLayer); // зарегистрировать слой

await jestLayer.mock('./foo', () => {
  // ...
}); // замокать модуль ./foo
await jestLayer.mock('./bar', () => {
  // ...
});
await jestLayer.runCode((foo, bar) => {
  console.log(foo, bar); // 123, '456'
}, [123, '456']); // выполнить функцию с указанными аргументами
```

В указанном примере регистрируется jest-слой, мокаются модули `'./foo'` и `'./bar'` и выполняется функция. Указанные
действия выполняются сразу в двух процессах - основном и дочернем.

> Обратите внимание, что действия в mirror выполняются с применением await. Это позволяет синхронизировать окончание выполнения действий в двух процессах.

> В консоли увидим два результата console.log - от основного и дочернего процессов

> Так же заметьте, что для передачи аргументов у `runCode` есть отдельный параметр. Замыканию работать не будут

### JestLayer

Слой для синхронизации среды исполнения jest

#### constructor(filename: string, jest: Jest)

- `filename` - имя файла с тестом
- `jest` - глобальный объект jest

#### mock(moduleName: string, moduleFactory: function, options?: MockOptions, callOptions?: CallOptions): Promise<CallResult<void>>

Мокает модуль (запускает [jest.doMock](https://jestjs.io/docs/jest-object#jestdomockmodulename-factory-options) в обоих
процессах)

- `moduleName` - имя модуля (см. докментацию
  к [jest.doMock](https://jestjs.io/docs/jest-object#jestdomockmodulename-factory-options))
- `moduleFactory` - функция мока (см. докментацию
  к [jest.doMock](https://jestjs.io/docs/jest-object#jestdomockmodulename-factory-options))
- `options?` - опции (см. докментацию
  к [jest.doMock](https://jestjs.io/docs/jest-object#jestdomockmodulename-factory-options))
- `callOptions?` - опции
  запуска ([CallOptions](https://github.yandex-team.ru/market/testament/blob/master/src/mirror/method.ts#L3))

#### requireModule(moduleName: string, callOptions?: CallOptions): Promise<CallResult<any>>

Подключает модуль (вызывает `require` в обоих процессах)

- `moduleName` - имя модуля
- `callOptions?` - опции
  запуска ([CallOptions](https://github.yandex-team.ru/market/testament/blob/master/src/mirror/method.ts#L3))

Возвращает подключенный модуль

#### runCode<TArg extends any[], TResult>(code: (...args: TArg) => TResult, args: TArg, filename?: string, callOptions?: CallOptions): Promise<CallResult<TResult>>

Запускает код в обоих процессах

- `code` - функция, которую нужно запустить
- `args?` - аргументы, которые будут переданы в функцию
- `filename?` - имя файла, которое будет отображаться в стек-трейсе
- `callOptions?` - опции
  запуска ([CallOptions](https://github.yandex-team.ru/market/testament/blob/master/src/mirror/method.ts#L3))

Возвращает результат вызова функции

### MandrelLayer

#### constructor(config?: Config)

- `config.resourcesPath: string` - путь как директории с ресурсами
- `config.envConfig: object` - карта бекендов и их хостов
- `config.showResourceLog?: boolean` - показывать логи ресурсов (по умолчанию `false`)
- `config.defaultRoutes?: object` - дефолтные роуты для роутера (стандартный формат сусанина)

#### initContext(params?: InitContextArg): Promise<Context | null>

Создать mandrel-контект

- `params?` - параметры
  контекста ([InitContextArg](https://github.yandex-team.ru/market/testament/blob/a5e6c473edbe118d4b0f796d39155d8eb4a8a819/src/mirror/layers/mandrel/contextHelpers.ts#L74))

### KadavrLayer

__Внимание!__ В новой версии testament по умолчанию отключено сетевое взаимодействие kadavr layer'a - то есть поведение аналогичное прошлому `kadavrAsLibrary: true`.

#### constructor(config: Config)

- `config.host: string` - хост, на котором поднят кадавр
- `config.port: number` - порт, на котором поднят кадавр

#### getSessionId(): string | null

Получить ID сессии

#### setState<TData>(path: string, data: TData): Promise<void>

Установить kadavr-стейт

- `path` - путь стейта
- `data` - данные для стейта

### ApiaryLayer

#### mountWidget<TWidgetProps>(pathToWidget: string, props?: TWidgetProps | ()=>TWidgetProps): Promise<MountWidgetResult>

Рендерит виджет и монтировать в JSDOM

- `pathToWidget` - путь к виджету
- `props?` - данные для виджета или функция для формирования данных

Возвращает:

- `html: string` - Разметка виджета
- `container: HTMLElement` - DOM-контейнер в который смонтирован виджет
- `http.status: Array<{code: number; lock: boolean}>`- список HTTP-статусов выставленные виджетов
- `http.headers: Array<{name: string; value: string}>` - список HTTP-заголовков выставленные виджетов
- `data: unknown` - данные, которые вернул контроллер виджета

Полноценный кейс тестирования виджета можно увидеть на
примере [AdultWarning](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.desktop/widgets/content/AdultWarning/__spec__/index.spec.js).

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
import {PackedFunction} from '@yandex-market/testament/mirror';

apiaryLayer.mountWidget(
    './widget',
    new PackedFunction(
        (foo, bar) => ({
            fooValue: foo,
            barValue: bar,
            // ...some other async madness
        }),
        ['foo value', 'bar value'],
    ),
);
```

## Тестирование эпиков

Задача эпиков - генерировать action'ы в ответ на другие action'ы

Не смотря на то, что эпики неявно тестируются во время взаимодействия с view виджета, тем не менее вы можете
протестировать эпик в отрыве от виджета.

Эпики apiary-виджетов параметризируются объектом с данными о параметрах виджета и коллекциями.

Для воспроизведения этого поведения testament содержит хелпер для запуска эпиков.

__epics.spec.js:__

```js
import createEpicExecutor from '@yandex-market/testament/platform/apiary/epicExecutor';

const callEpic = createEpicExecutor(widgetData, collections)(epic);

describe('expConfirm', () => {
    it('reload должен приводить к перезагрузке страницы', async () => {
        const action = await callEpic(expConfirm({ reload: true })).toPromise();

        expect(action).toMatchSnapshot();
        expect(window.location.reload).toHaveBeenCalled();
    });
});
```

В примере выше мы покрываем результат вызова эпика снапошотом и убеждаемся в том, что `window.location.reload` был
вызван

## Тестирвование контролеров

Если хочется отдельно протестирвать логику контроллера, то это можно сделать следующим образом:

```js
import { mockContext } from '@yandex-market/testament/platform/mandrel/mock';
import controller from './controller';

beforeAll(async () => {
    await mandrelLayer.initContext({});
});

it('должен генерировать верные данные, коллекции и слоты', async () => {
    const getContext = require('@yandex-market/mandrel/mockedContext');
    const schema = controller(getContext(), inputOptions);

    expect(schema.data).toMatchSnapshot();
    expect(schema.collections).toMatchSnapshot();
    expect(schema.slots.foo.name).toBe('@marketfront/Foo');
    expect(schema.slots.bar.name).toBe('@marketfront/Bar');
});
```

## Allure-отчет

Если необходим отдельный allure-отчет, то добавить в jest-конфигурацию:

```
{
    reporters: [
        'default',
        '@yandex-market/testament/reporter/allure',
    ],
}
```

По умолчанию, отчет будет сохранен в директорию `html_reports/allure`, для изменения директории используйте
параметр `saveTo`:

```
{
    reporters: [
        'default',
        ['@yandex-market/testament/reporter/allure', {
            saveTo: 'path/to/report-dir',
        }],
    ],
}
```

## Ускорение резолвинга файлов
Под капотом у jest происходит множество полезной работы.
Например, для корректной работы `jest.mock` jest часто ходит в файловую систему, что чревато увеличением времени
прохождения тестов на каждом `import` или `require`.
Для решения данной проблемы можно использовать in-memory файловую систему, которая будет использовать оперативную память
для хранения структуры реальной файловой системы. Таким образом, вместо походов в файловую систему,
jest будет "ходить" в оперативную память (по крайней мере для резолвинга путей import'ов и require'ов),
что в разы быстрее.

Особо актуальна данная функциональность при работе в Аркадии,
в которой время прохождения тестов может быть заметно больше, чем вне ее.

В приложении marketfront инициализация in memory файловой системы уже выполняется при прогоне testament тестов,
ничего дополнительно делать не нужно. Карту файлов для marketfront можно перегенерить через `npm run test:dumpfs` из
папки платформы. В случае добавления новых файлов, отсутствующих в карте, resolver возьмет их из
реальной файловой системы, поэтому хорошей практикой будет перегенерить карту,
когда хождения в реальную fs будут слишком частыми.

<details><summary>Как это работает - для интересующихся:</summary>

In memory fs реализована с помощью https://www.npmjs.com/package/memfs

Что нужно сделать, чтобы инициализировать in memory файловую систему:

__Создать карту файлов приложения в реальной файловой системе.__

Создать можно таким скриптом (он же в маркетфронте `npm run test:dumpfs`):
```
  find ../.. -type file -not -path "*/.cache/*" > ../../fs_maps/fs_map.txt
```
И для симлинков:
```
  for filename in $(find ../.. -type l -not -path "*/.cache/*"); do
    echo "$filename:$(readlink $filename)" >> ../../fs_maps/fs_map.txt
  done
```

__Запустить jest testament тесты__
```
npm run jest:testament
```
По дефолту карта будет искаться в директории TESTAMENT_FS_MAP_LOCATION=../../fs_maps/fs_map.txt - при необходимости
эту энву можно переопределить.
</details>
