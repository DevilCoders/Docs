

### Песочница
```jsx harmony
import Button from '@self/root/src/uikit/components/Button';

initialState = {
    isPopupVisible: false,
};

const DefaultContent = () => (
    <React.Fragment>
        <h3>Тут могло быть содержимое попапа</h3>
        <p>Вместо этого, тут унылый текст</p>
    </React.Fragment>
)

const PopupModalExample = ({position, hasBackdropClose, children}) => {
    const togglePopup = () => setState({isPopupVisible: !state.isPopupVisible});
    const Content = Boolean(children) ? children : <DefaultContent />;

    return (
        <div>
            <Button onClick={togglePopup}>
                Открыть попап
            </Button>

            {state.isPopupVisible && (
                <PopupModal position={position} hasBackdropClose={hasBackdropClose} onClose={togglePopup}>
                    {Content}
                </PopupModal>
            )}
        </div>
    );
};

const props = {
    position: {
        required: false,
        type: 'enum',
        values: ['top', 'center', 'bottom'],
        defaultValue: 'center'
    },
    hasBackdropClose: {
        required: false,
        type: 'boolean',
        defaultValue: false
    },
    children: {
        require: false,
        type: 'string',
        defaultValue: '',
    }
};

<Helper.Playground
    component={PopupModal}
    example={props => <PopupModalExample {...props} />}
    props={props}
/>

```
