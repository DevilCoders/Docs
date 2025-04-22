### withPermissions(permissions, renderPlaceHolder) 
HOC для проверки необходимых прав у текущего пользователя.

#### permissions: array
Массив из строк вида 
```javascript
['superuser', 'main']
```
Если хотя бы одна из указаных ролей в **permissions** присутствует у пользователя, компонент, обернутый в HOC,  рендерится как есть, иначе на месте компонента рендерится результат функции **renderPlaceHolder**

#### renderPlaceHolder: function
Если аргумент **renderPlaceHolder** не был передан в HOC, вместо компонента возвращается `null`

### Пример использования
```javascript
class MyComponent extends React.Component {}

export default withPermissions(['superuser'], () => <Forbidden />)(MyComponent);
```