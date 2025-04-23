# persisted-data

## Описание:

High Order Component позволяющий организовать взаимодействие компонента с локальным хранилещем данных в браузере пользователя. 
Реализовано на базе [localforage](https://www.npmjs.com/package/localforage), тип хранилищиа (WebSQL, IndexedDB, localstorage) выбирается автоматически.

## Usage

```javascript
// undefined - если данные из localstorage еще не пришли (асинхронная операция еще не завершилась)
// null - если данные из localstorage пришли (асинхронная операция завершилась), но они пустые (falsy)
const mapDataToProps = (data: DataProps | undefined | null): DataProps => {
    return {
        prop: data && data.prop || {},
    };
};

const mapActionsToProps = (actions: PersistActions): ActionProps => {
    return {
        onAction: props => actions.change({ props }),
    };
};

export const orderReactionsListConnector = (
    component: React.ComponentType<Props>,
    key: string
) => {
    return withPersistentData(
        mapDataToProps,
        mapActionsToProps,
        { instanceName: localstorageInstanceName, key }
    )(component);
};
```

## API

Необходимо в функцию `withPersistentData` передать 2 функции и конфиг:
* `mapDataToProps` - функция для мержа данных компонента с данными из localstorage
* `mapActionsToProps` - функция для проброса actions в компонент и передачи функции `onChange`, при помощи которой мы сихронизируем данные. Данная функция принимает либо новое значение объекта в localStorage, либо функцию, в которой мы имеем доступ к старым данным и можем их обновить
* `PersistenceConfig` - конфиг, в котором можно передать название инстанса, ключ, по которому можно получить данные из localstorage, время частоты синхронизации (500мс по умолчанию)

На выходе получается HOC, из которого мы можем получить persistedComponent, передав в него наш компонент


## Important Notes
При изменении содержимого localstorage (то есть вызова функций `actions.change()`), компонент будет перерендерен со старым значением (тем что было получено после первого обращения к localstorage) `data` в `mapDataToProps`.

[Пример использования](https://github.yandex-team.ru/search-interfaces/frontend/blob/1e1b4743c9220de65b510f83112e45a44ef854c6/services/ydo/src/components/forms/Order/connectors/createOrder.ts#L176)

