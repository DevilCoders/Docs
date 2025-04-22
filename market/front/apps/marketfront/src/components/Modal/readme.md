# Modal

Ещё одна имплементация Modal'ного окна.
По сути является пресетом настроек `PopupBase`.
 Отличается от остальных пресетов:
- шириной по контенту и правильным положением скролла при вылезании за границы экрана
- наличием пропсы `visible`, отвечающей за появление.

На click по паранже модалка попытается закрыться.


```jsx noeditor
import Button from '@self/root/src/uikit/components/Button';

initialState = {visible: false};
const toggle = () => setState({visible: !state.visible})

const Example = props => {
    return (
        <div>
            <Button onClick={toggle}>Открыть попап. Галка `visible` должна быть прожата</Button>
            <Modal {...props} visible={state.visible && props.visible} onClose={toggle}>
                {props.children}
            </Modal>
        </div>
    );
}

const DefaultChildren = () => (
    <div>
        Содержимое модалки
        <br/>
        such modal
        <br/>
        much wow
        <br/>
        such modal
        <br/>
        much wow
        <br/>
        such modal
        <br/>
        much wow
        <br/>
        such modal
        <br/>
        much wow
        <br/>
        such modal
        <br/>
        much wow
        <br/>
        such modal
        <br/>
        much wow
        <br/>
        such modal
        <br/>
        much wow
        <br/>
        such modal
        <br/>
        much wow
        <br/>
        such modal
        <br/>
        much wow
        <br/>
        such modal
        <br/>
        much wow
        <br/>
        such modal
        <br/>
        much wow
        <br/>
        such modal
        <br/>
        much wow
        <br/>
        such modal
        <br/>
        much wow
        <br/>
        such modal
        <br/>
        much wow
    </div>
);

<Helper.Playground
    component={Modal}
    example={Example}
    defaultValues={{
        children: (<DefaultChildren/>),
        hasCloser: true,
        visible: true,
    }}
/>

```
