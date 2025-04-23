# DropdownMenu

Всплывающее меню

Компонент состоит из меню, пунктов меню (поддиректория Item) и кнопки, при нажатии на которую появляется меню.

Пример использования:
```javascript
const DropdownMenu = require('@self/platform/components/DropdownMenu').default;
const DropdownMenuItem = require('@self/platform/components/DropdownMenu/Item').default;

<div style={{width: '200px'}}>
    <DropdownMenu>
        <DropdownMenuItem text="Удалить" onClick={() => console.log('delete')} />
        <DropdownMenuItem text="Отредактировать" onClick={() => console.log('edit')} />
    </DropdownMenu>
</div>
```
