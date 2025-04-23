## makeConditionRendererHOC
```javascript
makeConditionRendererHOC({predicate, selector, omitProps, renderPlaceHolder})
```
Функция для создания простых HOC, используемых для изменения отображения компонента в зависимости от состояния данных в **ReduxStore** или собственных свойств компонента

#### predicate: function
Вызывается со всеми свойствами компонента и должна возвращать тип Boolean
```javascript
const predicate = props => props.user.superuser ? true : false;
```
Если результат выполнения **predicate(props)** равен **true**, компонент, обернутый в HOC, рендерится как есть, иначе на месте компонента рендерится результат функции **renderPlaceHolder**

#### selector: function | reselect
Селектор для передачи в компонент необходимых данных из **ReduxStore**

#### omitProps: array
Массив ключей, которые не должны попасть в свойства компонента

#### renderPlaceHolder: function

Если аргумент renderPlaceHolder не был передан, вместо компонента будет возвращаться **null**

### Пример использования
```javascript
const withPermissions = function (permissions, renderPlaceHolder) {
    return makeConditionRendererHOC({
        selector: createSelector(state => ({user: state.user}), identity),
        omitProps: ['user'],
        predicate: props => permissions.some(rule => props.user[rule]),
        renderPlaceHolder
    });
}
```