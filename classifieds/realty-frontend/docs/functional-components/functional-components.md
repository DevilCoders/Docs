# Функциональные компоненты

Мир не стоит на месте, React развивается и там все больше идет упор на функциональные компоненты. 
Вплоть до того, что новые фичи будут доступны только для них. 

Кроме того функциональные компоненты должны быть более производительными, благодаря тому, что дерево компонентов не раздувается из-за хоков.

Поэтому в новом коде всегда предпочтительнее использовать функциональные компоненты, чем классовые. Попутно добавляя хуки взамен использующихся хоков.

Далее описаны соглашения о том, как нужно писать функциональные компоненты.

## Контекст
Контекст, селектор контекста и управление контекстом лежат в одном файле
```typescript
interface ISomeContextValue {}

const SomeContext = React.createContext<ISomeContextValue | null>(null);

export const useSomeContext = () => {
    const value = React.useContext(SomeContext);
    return value;
};

interface ISomeContextProviderProps {}

export const SomeContextProvider: React.FC<ISomeContextProviderProps> = ({ children }) => {
    const value = React.useMemo<ISomeContextValue>(() => {
        // ...
    }, []);
    return (
        <SomeContext.Provider value={value}>
            {children}
        </SomeContext.Provider>
    );
};
```

## Файловая структура компонентов
Хуки лежат отдельно от компонентов.
Рядом с компонентом создается папка `hooks`, куда можно сложить все хуки. 
Каждый хук должен быть связан только с одной частью бизнес-логики. 

Один хук - один файл. Имя файла = название хука.

Общие хуки для складываем в ```realty-core```
- Хуки связанные с какой-то конкретной предметной областью складываем в соответствующий модуль ```realty-core/view/react/modules```
- Хуки, использующиеся повсеместно в `realty-core/view/react/common/hooks`


Пример структуры компонента
```typescript
const UserPopup: React.FC = () => {
    const {} = useUserPopup();
    const {} = useUserPopupStats();
    
    return <div />
};
```

```
User
    UserPopup
        index.js
        hooks
            useAuth.js
            useUserPopupStats.js
    UserAccounts
        index.js
        hooks
            useUserAccounts.js
    index.js
    hooks
        useUserData.js

```
## Мемоизация 
Всегда используем `React.memo` за исключением случаев, когда компонент имеет children в пропсах (реакт возвращает не ссылку на компоненты а всегда новый объект [пруф](https://github.com/facebook/react/blob/1ad8d81292415e26ac070dec03ad84c11fbe207d/packages/react/src/ReactElement.js#L149))

```typescript
const MemComp = React.memo(({ a, b, c }) => {
    // ...
    return <div></div>;
});

const ComponentWithChildren = ({ a, b, c, children }) => {
    // ...
    return <div></div>;
};

// в следующем случае нет смысла в том, чтобы Comp был мемоизированный, так как в любом случае перерисуется
<Comp>
    <ChildComp />
</Comp>
```

`useCallback` и `useMemo` используем для того, чтоб не передавать ссылочные типы данных вниз по дереву (это будет триггерить перерисовки)
Так же `useMemo` стоит использовать для мемоизации сложных вычислений

```typescript
const Comp = React.memo(({ a, b }) => {
    const cb = useCallback(() => {}, []);
    const complexProp = useMemo(() => {
        return {
            a: 'a',
            b: 'b',
        };
    }, []);

    const computedString = useMemo<string>(() => complexCalculations(), []);

    return (
        <>
            <button onClick={() => {}}/>

            <Component
                onClick={cb}
                complexProp={complexProp}
                easyProp={`${a}-${b}`}
                computedString={computedString}
            />
        </>
    );
});
```

## Дефолтные значения
- defaultProps с функциональными компонентами не используем
- При определении дефолтного значения ссылочных типов данных не используем литералы - выносим их в константы (исключением является `null`)

Пример:

```typescript
    const defaultObj = {};

    const Component = ({
        // плохо - ссылочные типы данных
        prop1 = {},
        prop2 = () => {},
        prop3 = [],
        // хорошо - ссылочные типы данных, ссылки на которые не меняются
        prop35 = defaultObj,
        prop6 = null,
        // хорошо - примитивы (можно сравнивать строгим сравнением)
        prop4 = '',
        prop5 = 0,
        prop7 = undefined
    }) => {
        // ...
    };

    // deprecated - не работает с ts
    Component.defaultProps = {};
```

## Обработка ошибок
Оборачиваем в [ErrorBoundary](../../realty-core/view/react/common/components/ErrorBoundary/index.tsx) только компоненты, которые можно назвать самостоятельной фичей.
Фича - это, самостоятельный компонент, не зависящий от родительского, при этом родительский компонент может полноценно функционировать без него.

Не имеет смысла оборачивать маленькие компоненты.

В `ErrorBoundary` нужно оборачивать компонент при использовании, а не внутри его рендера (это позволит отловить ошибки внутри хуков).

Плохой пример:
```typescript
    const SiteCardForm = () => {

        return (
            <form onSubmit={() => {}}>
                <ErrorBoundary>
                    <Button>submit/Button>
                </ErrorBoundary>
                <ErrorBoundary>
                    <Input name="name1" />
                </ErrorBoundary>
                <ErrorBoundary>
                    <Input name="name2" />
                </ErrorBoundary>
            </form>
        );
    };
```

Хороший пример:
```typescript
    import { ErrorBoundary } from 'realty-core/view/react/common/components/ErrorBoundary'


    const SiteCard = () => {
        return (
            <>
                <ErrorBoundary>
                    <SiteCardForm />
                </ErrorBoundary>
                <ErrorBoundary>
                    <SiteCardGallery />
                </ErrorBoundary>
                <ErrorBoundary>
                    <SiteCardGenPlan />
                </ErrorBoundary>
                <ErrorBoundary>
                    <SiteCardSimilar />
                </ErrorBoundary>
                <ErrorBoundary>
                    <SiteCardReviews />
                </ErrorBoundary>
            </>
        );
    };
```

Более сложный пример:

Есть фильтры
![filters](./filters.png)
Тут помимо оборачивания всех фильтров есть смысл обернуть такие компоненты как:
- Геоселектор (там много логики: модалки с выбором метро, области на карте и др.)
- Виджет "Сохранить поиск"

НЕ стоит оборачивать каждый контрол в отдельности
