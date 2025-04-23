# Modal
Использования для создания модальных окон. [Подробнее](https://ru.bem.info/libs/bem-components/v2.3.0/desktop/modal/)

## Использование
```jsx
var Modal = require('bem-react/lib/Modal');

var handleModalClose = function() {
    console.log('Modal is closed');
};

<Modal closable={true} onClose={handleModalClose} visible={this.state.showModal}>
    <h3>Some content goes there</h3>
</Modal>
```

## Методы

#### open()
Открывает диалог

#### close()
Закрывает диалог

## Параметры

#### closable `Boolean`
Включает возможность закрыть окно по клику на оверлей или нажатием <kbd>Esc</kbd>

#### onClose(payload)
Колбэк закрытия модального окна
- **payload** `Object`
  - **target** `BEM`
    Экземпляр BEM блока

#### onOpen(payload)
Колбэк открытия модального окна
- **payload** `Object`
  - **target** `BEM`
    Экземпляр BEM блока

#### theme `String`
Тема: `islands`

#### visible `Boolean`
Делает модальное окно видимым

#### zIndex `Number`
