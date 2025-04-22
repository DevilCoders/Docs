Компонент Dropdown
---

Сочетание 2 элементов:
- кнопки
- попапа

По умолчанию рисуется кнопка со стрелкой по нажатии на которую, снизу выпадает попап с содержимым
из children

Выглядит так

![example.png](./example.png)

Ссылки:
---

stories: https://yandexclassifieds.github.io/realty-frontend/vertis-react/?selectedKind=Components%7CDropdown&selectedStory=dropdown

Кастомизация
---
Компонент принимает функции для рендера кнопки и самого попапа `renderButton` и `renderPopup` соответственно.

Благодоря этому можно довольно сильно кастомизировать его поведение. В частности, можно вместо кнопки рисовать иконку.

Функции рендеринга имееют следующие сигнатуры:
```ts
type ButtonHandlers = {
    handleRef: () => void,
    handleClick: () => void,
    handleKeyDown: () => void,
    handleFocusChange: () => void,
    handleMouseEnter: () => void,
    handleMouseLeave: () => void,
};

function renderButton(props: DropdownProps, state: DropdownState, handlers: ButtonHandlers): JSX.Element;

type PopupHandlers = {
    handleMouseEnter: () => void,
    handleMouseLeave: () => void,
};
function renderPopup(props: DropdownProps, state: DropdownState, handlers: PopupHandlers): JSX.Element;
```

---
**ВАЖНО**:

`renderButton` - должен вернуть компонент, а не любой jsx, потому что Dropdown лезет в `this._control.refs.control`
---

Также можно передать свои props для попапа через `popupProps`

Показ по ховеру
---
С помощью пропсы `showOnHover` можно заставить попап появляться по ховеру, а не по клику.

Посмотреть можно тут: https://yandexclassifieds.github.io/realty-frontend/vertis-react/?selectedKind=Components%7CDropdown&selectedStory=showOnHover
