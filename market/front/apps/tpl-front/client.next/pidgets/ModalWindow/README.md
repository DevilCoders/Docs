# ModalWindow (пиджет)

Это модальное окно - обертка над ModalWindow из levitan, синхронизирующая свое состояние через коллекцию abstractModal.

## Использование

Компонент принимает те же пропсы, что и ModalWindow из levitan. Отличия:

- требует указать уникальный `id` типа AbstractModalId.
- открывается и закрывается с помощью единых экшенов (см. ниже).
- атрибут `isOpen` - опциональный, его использование переводит модалку в контролируемый режим.
- имеет опциональный атрибут `queryable`, при активности которого открытость модалки будет синхронизироваться с параметрами url.

Пример использования:
```js
import {ModalWindow} from '~/pidgets/ModalWindow';

<ModalWindow id={CASHBACK_MODAL_ID} queryable={true}>
    <Content />
<ModalWindow>
```

### Создание id

Id можно создать с помощью функции `createModalId ` возвращающей уникальный id типа `AbstractModalId`. Эта функция принимает строку в формате `<scope>:<feature>`, где scope - область применения модалки (страница или виджет, компонент), feature - ее назначение. Если id уже занят - выкидывает ошибку.

Пример:
```ts
import {createModalId} from 'shared/collections/abstractModal';

export const CASHBACK_MODAL_ID = createModalId('CustomPromoCashbackModal:editPromo');
```

### Экшены для открытия и закрытия
Открывается и закрывается модалка с помощью экшенов `modalAction`.
Эти экшены принимают id модалки и их использование приводит к изменению свойств соответствующей сущности в коллекции.

При открытии модалки так же можно указать id контента, который надо отобразить (подробнее ниже).

Пример:
```js
import {modalAction} from '~/actions/modalWindow';

const AddGroupButton = ({contentId}) => {
    const openModal = useAction(() => {
        return modalAction.open({id: CASHBACK_MODAL_ID, contentId})
    });

    return <Button onClick={openModal}>Click!</Button>
};
```

### Хук для получения получения данных
Если контент модального окна должен представлять содержимое некой колекции, то стоит воспользоваться хуком `useModalContent` или `useModalContentId`.

Этот хук принимает селектор коллекции, и возвращает сущность, id которой был указан при вызове экшена открывающего окно (`contentId`). 

Под капотом хук является оберткой над useSelector и useContext, с помощью которых извлекаются данные, релевантные модалке, частью которой является текущий компонент.

Пример использования:
```ts
import {useModalContent} from '~/hooks/modalWindow'

export const Content = () => {
    const draft = useModalContent(selectModalDraftCollection);
    ...
}
```

Хук имеет два режима: не гарантирующий наличие контента и гарантирующий, но в случае отсутствия контента вызывающий закрытие модалки и вывод ошибки в консоль.

Это определяется опциональным аргументом `safe`. Пример:
```ts
const entity: Entity | undefined = useModalContent(selectCollection)

const entity: Entity = useModalContent(selectCollection, true) 
```

