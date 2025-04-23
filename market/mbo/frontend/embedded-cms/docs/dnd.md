# Drag and drop

В каждый renderer приходит объект dnd и 2 компонента: DndSource и DndTarget.

Types:
```flow js
/**
* isEnter - На текущий элемент навели какой то узел
* isDragged - Текущий элемент куда то перетаскивают
*/
type dnd = {
  isEnter: boolean,
  isDragged: boolean
}

/**
* children - Контент области за которую можно тащить узел
* classNames - Классы которые будут навешаны на компонент DndSource
* classNamesDndContainer - Классы которые будут навешаные на preview при переносе
* preview - HTML елемент который будет отображаться в preview при переносе.
*           Если значение не было указано, в качестве preview используется
*           обертка над рендерером.
*/
type DndSourceProps = {
  children: JSX.Element,
  classNames?: string,
  classNamesDndContainer?: string,
  preview?: HtmlElement
}

/**
* children - Контент области в которую можно дропнуть другой узел.
* classNames - Классы которые будут навешаны на компонент DndTarget
*/
type DndTargetProps = {
  children: JSX.Element,
  classNames?: string
}
```

Перемещения можно осуществлять только в рамках одного массива.