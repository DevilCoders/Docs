# withReduxState

high order component для
- подключения данных из `Reudx`
- подключения `actions` обернутых в `dispatch`

Смотри также: [core/state/](../../core/state/README.md)

```ts

type TSelector<S, P> = (state: S, ownProps: P) => Partial<P>
type TWrapper<P> = (WrappedComponent: React.ComponentClass<P>) => React.ComponentClass<P, Partial<P>>

/**
 * Подключение объекта к Redux. Примерно как redux-react/connect
 *
 * @param stateToProps - функция получения данных из store
 * @param dispatchToProps - объект [key: ActionCreator]. Результат ActionCreater будут
 * сразу передаваться в store.dispatch
 */
function withReduxState<IProps, IStore>(
    stateToProps: TSelector<IStore, IProps>,
    dispatchToProps?: Partial<IProps>
): TWrapper
```


## Пример

**Задача**:

Необходимо сделать компонент `<ItemInMyCart />`, который
- показывает кол-во товарова в корзине
- может добавить еще товар при клике
- может очистить корзину

_Примечание_: Считаем, что редьюсер и какая-то бизнел-логика [успешно добавлены](../../core/state/README.md), осталось компонент связать

---
**actions.ts**
```ts

/**
* События а-ля FLA
* @see https://github.com/redux-utilities/flux-standard-action
*/

export function deleteItems() {
    return {
        type: 'CART/CLEAR'
    }
}

export function addItem(item: ICartItem) {
    return {
        type: 'CART/PUSH_ITEM',
        payload: { item }
    }
}
```

---

**selectors.ts**
```ts
/**
 * Селекторы нужны чтобы:
 *  - знания о структуре стора были для потребителя не важны
 *  - возможность кешировать вызовы
 */

export function getState(state: IReduxStore) {
    return state.cart || initialState;
}

export function getItems(state: IReduxStore): ICartItems[] {
    return getState(state).items || [];
}

export function getItem(state: IReduxStore, id: string): ICartItem | undefined {
    return getItems(state).filter(item => item.product.id === id)[0];
}
```

---

**ItemInMyCart.ts**
```ts
import { ICartItem } from '@yandex-turbo/components/CartData/CartData.types';
import { withReduxState } from '@yandex-turbo/components/withReduxState/withReduxState';
import { getItem } from '@yandex-turbo/core/state/cart/selectors';
import { addItem, deleteItems } from '@yandex-turbo/core/state/cart/actions';

interface IProps {
    // Товар, который захотим положить в корзину
    currentItem: ICartItem,
    // Товар в корзине
    itemInCart?: ICartItem,
    // Очистить всю окрзину
    deleteItems?: () => void;
    // Добавить item в корзину
    addItem?: (item: ICartItem) => void;
}

/**
 * Компонент, который
 *   - показывает кол-во товарова в корзине
 *   - может добавить еще товар при клике
 *   - может очистить корзину
 */
class ItemInMyCart extends React.Component<IProps> {
    public render() {
        const { currentItem, count = 0 } = this.props;

        return (
            <>
                Товар: {currentItem.product.title}; В корзине: {
                    temInCart ? itemInCart.count : 0
                } шт.
                <hr/>
                <button onClick={this.handleClickAdd}>Еще ➕</button>
                <button onClick={this.handleClick}>Удалить все ❌</button>
            </>
        )
    }

    private handleClickAdd = () => {
        const { addItem, currentItem } = this.props;

        if (addItem) {
            addItem(currentItem); // eq: store.dispatch({ type: 'CART/PUSH_ITEM', payload: { item: currentItem } })
        }
    }

    private handleClick = () => {
        const { deleteItems } = this.props;

        if (deleteItems) {
            deleteItems(); // eq: store.dispatch({ type: 'CART/CLEAR' })
        }
    }
}

export withReduxState<IProps>(
    (state, ownProps) => ({
        itemInCart: getItem(state, ownProps.currentItem.productId)
    }),
    {
        deleteItems,
        addItem
    }
)(ClearMyCart)
```
