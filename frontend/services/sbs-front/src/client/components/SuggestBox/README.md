## SuggestBox
Компонент используется получения списка предложений по строковому запросу.

### Пример использования
Допустим у нас есть функция ```fetchUsersByName``` которая возвращает массив объектов с ключами ```name```, ```age```. Функция может быть асинхронной для получения данных сервера.
Ниже пример кода использования компонента.
```jsx
<SuggestBox
    getter={ (query) => fetchUsersByName(query) }
    transform={ (user) => user.name }
    onChange={ (transformedUser, user) => saveSelectedUser(transformedUser) }
    onBlur={ () => this.onBlur() }
    disabled={ disabled }
    text="Начните вводить имя пользователя..."
>
    { (userName, { source:user, selected }) => (
        <Bem block={ block } elem="User" mods={ { selected } }>
            <Bem block={ block } elem="UserName">
                { transformedUser }
            </Bem>
            <Bem block={ block } elem="UserAge">
                <Username username={ user.age }/>
            </Bem>
        </Bem>
    ) }
</SuggestBox>
```

### Props
#### getter
Указывает функцию для получения данных. Например:
```javascript
const sugggestUsers = query =>
    users.filter(user => user.name.includes(query));
```

```javascript
const sugggestUsers = async (query) => {
    return await(await fetch(`https://example.net/api/users?q=${ query }`, {
        method: 'GET',
    })).json();
};
```
#### transform
Указывает функцию для получения данных. Например:
```javascript
const getUserName = user => user.name
```

#### onChange
Колбек, вызывается при изменении данных. Первым аргументов возваращет данные на основе функции ```transform```, вторым – полный объект списка
```javascript
onChange = (userName, user) => { ... }
```

#### onBlur
Колбек, вызывается при ухода фокуса с элемента.

#### disabled
Указывает заблокировано ли поле

#### text
Текст для поисковой строки, когда она пуста.

#### children
Функция, которая используется при рендеринге элементов списка, первый аргумент функции - результат применения функции ```transform``` к выбранному элементу, вторым аргументом указывается объект с дополнительными данными:
```javascript
{
    source, // Исходный элемент до применения transform
    selected // Указывает является ли данный элемент выбранным
}
```
По умолчанию каждый элемент рендерит ```String(item)```. Можно изменить поведение по умолчанию с помощью пропса ```title```, который описан ниже.

#### title
Функция, которая используется, если не задано ```children```. Например, если мы хотим, чтобы каждый эелемент списка был строкой с логином пользователя + его именем, то:
```javascript
const getUserName = user => `${ user.login }: ${ user.name }`
```

