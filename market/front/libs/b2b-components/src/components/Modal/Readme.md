Модальное окно

```jsx
initialState = {isOpen: false};
show = () => setState({isOpen: true});
close = () => setState({isOpen: false});

<div>
    <Button onClick={show}>Нажми на меня</Button>

    <Modal isOpen={state.isOpen} close={close}>
        <div>
            Контент модального окна
        </div>
    </Modal>
</div>
```

Без закрывающего крестика

```jsx
initialState = {isOpen: false};
show = () => setState({isOpen: true});
close = () => setState({isOpen: false});

<div>
    <Button onClick={show}>Нажми на меня</Button>

    <Modal isOpen={state.isOpen} closable={false}>
        <Button onClick={close}>Закрыть</Button>
    </Modal>
</div>
```
