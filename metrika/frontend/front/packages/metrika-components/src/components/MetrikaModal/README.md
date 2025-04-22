Модальное окно с кастомной анимацией. Также есть возможность показа крестика для закрытия
Имеет те же свойства что Modal из лего + дополнительный callback onCloseButtonClick и prop closable

```(jsx)
const { Button } = require('lego');

initialState = {
    visible: false,
};

<div>
    <Button
        onClick={() => setState({visible: true})}
        theme="normal"
        size="s"
    >
        Open
    </Button>
    <MetrikaModal visible={state.visible} onCloseButtonClick={() => setState({visible: false})}>
        <div>
            <br/>
            <br/>
            Содержимое модального окна
            <br/>
            <br/>
        </div>
    </MetrikaModal>
</div>
```
