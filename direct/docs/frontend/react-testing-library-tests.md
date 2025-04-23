# Содержание
- [Что из себя представляют react-testing-library (RTL) тесты](#info)
- [Как запустить RTL тесты](#run)
- [Как написать новый тест](#new-test)
- [Как производить отладку упавших тестов](#debug)
- [FAQ](#faq)

## Что из себя представляют react-testing-library (RTL) тесты { #info }
Это такие тесты, для работы которых используется библиотека [React-Testing-Library](https://testing-library.com/docs/react-testing-library/intro/).

Они являются модульными (unit) тестами т.к. исполняются в дешевой среде (без внешних зависимостей - без браузера, без участия бэкенда и без участия сторонних сервисов).

С помощью библиотеки RTL компонент монтируется в память над которым можно совершать любые пользовательские сценарии: кликать на элементы, писать текст и тд.

## Как запустить RTL тесты { #run }
RTL тесты являются подмножеством существующих модульных тестов, для запуска которых используется единая команда:
- `npm run unit` – запускает все модульные тесты
- `npm run unit StrategiesEditorBodyContainer.spec.tsx` - запускает все модульные тесты для указанного файла

## Как написать новый тест { #new-test }
Шаг 1. Для тестирования какого-либо компонента требуется сформировать только нужное состояние приложения (partialState) соответствующее начальному состоянию компонента, например:
```
const strategy = makeStrategyTypeOptimizeCpa();
const { partialState } = makePartialStateDataForStrategy({ strategy });
```

Шаг 2. Нужно смонтировать компонент в память используя функцию `renderTestScreen` передав 1 аргументом сам компонент, а вторым аргументом объект с полем partialState (этот объект также позволяет указывать дополнительные данные, например мок для graphql - см интерфейс 2 аргумента).
Пример:
```
renderTestScreen(
    <StrategiesEditorBodyContainerForTest campaignId={campaign.id} constants={strategy.constants} />,
    { partialState }
);
```
После того, как компонент смонтирован, можно вывести в консоль содержимое компонента, переданного в функцию `renderTestScreen` с помощью команды `screen.debug()`, где screen это функция из библиотеки (`import { screen } from '@testing-library/react';`).
```
renderTestScreen(...);
screen.debug();
```

Если отрисовывается большой компонент, то дефолтный html вывод в консоль может не поместиться, тогда можно поступить другим образом:

Вариант №1: Использовать `container.innerHTML`, пример:
```
const { container } = renderTestScreen(...);
console.log(container.innerHTML);
```

Вариант №2:
Использовать функцию `screen.logTestingPlaygroundURL()` ([документация](https://testing-library.com/docs/queries/about#screenlogtestingplaygroundurl)), пример:
```
renderTestScreen(...);
screen.logTestingPlaygroundURL(); // выведет ссылку в консоль, пройдя по которой можно увидеть весь отрисованный компонент

expect(...)
```


После того, как убедились, что компонент отрисовался ожидаемым образом, можно приступать к написанию взаимодействия с компонентом, например:
```
// кликаем на нужный текст
userEvent.click(screen.getByText('Подключить'));
// проверяем, что компонент отреагировал корректно
expect(screen.getByText('Подключено')).toBeInTheDocument();
```

## Как производить отладку упавших тестов { #debug }
Если тест упадет, то в выводе будет указано место в коде, где произошла ошибка (например, отсутствовали необходимые данные). Достаточно указать console.log в интересующем месте кода и запустить тест еще раз.
Если хочется в тесте сделать точку остановки и посмотреть в браузере, что в данный момент происходит в тесте, то можно поступить следующим образом:
1) В интересующем месте кода пишем `debugger`
2) Запускаем тест с помощью инспектора nodejs: `npm run unit:debug StrategiesEditorBodyContainer.spec.tsx` (аналогично стандартному запуску `npm run unit StrategiesEditorBodyContainer.spec.tsx`)
3) Открываем страницу [browser://inspect](browser://inspect) и жмем на `inspect`
    ![inspect](./assets/browser-inspect.png)

4) После этого мы оказываемся в браузере, в котором нужно разрешить выполнение скрипта из-за того, что тест запущем с флагом `--inspect-brk` (флаг из-за которого тест ожидает подключение через браузер)
    ![inspect](./assets/browser-debug.png)
5) Дождаться остановки в ранее указанном месте с помощью `debugger`

## FAQ { #faq }
1. Какие поисковые [запросы](https://testing-library.com/docs/queries/about) можно использовать в тестах


2. Почему расширение RTL тестов `.spec.ts`, а не `.test.ts`, как у остальных модульных тестов?

    Для файлов с расширением `.test.ts` выключена проверка типов.
    Если для этих файлов включить проверку, то выяснится, что существует множество проблемных мест, которые в рамках создания RTL тестов править не хотелось.
    Для RTL тестов проверка типов является неотъемлимой частью т.к. проверяется валидность подготовленных данных для отрисовки компонентов.


3. Можно мокать graphql запросы? - Да

    Для моков graphql используется библиотека [graphql-tools](https://graphql-tools.com/docs/mocking).

    Пример мока query запроса:
    ```
    const resolvers = {
        GdClient: {
            smartFilters: (_: void, v: Record<string, unknown>) => {
            return response.data.client.smartFilters;
        }
        }
    };
    ```
    Пример мока mutation запроса:
    ```
    const resolvers = {
        Mutation: {
            deleteFilters: (_: void, v: { input: GdDeleteSmartFilterInput }) => {
                return {
                    deletedItems: v.input.deleteItems,
                    validationResult: null
                };
            }
        }
    };
    ```
    После создания `resolvers` его нужно передать в функцию `renderTestScreen`:
    ```
    renderTestScreen(<Component/>, { resolvers })
    ```
4. Можно мокать action-ы - Да
    
    Пример mock-а action-а
    ```
    const { getActionMock } = renderTestScreen(
        <Component/>
    );

    const myActionMock = getActionMock(myAction);
    ```    
