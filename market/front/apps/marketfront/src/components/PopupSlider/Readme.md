
```jsx
import Button from '@self/root/src/uikit/components/Button';
import PopupSlider from '@self/root/src/components/PopupSlider';

initialState = {
    popupBottom: false,
    popupRight: false,
    popupWithoutParanja: false,
    popupWithoutBackdropHandler: false,
};

const togglePopup = (name) => setState({[name]: !state[name]});

const style = {marginTop: 20};

<div>
    <div style={{marginTop: 20}}>
        <Button onClick={() => togglePopup('popupBottom')}>Popup снизу</Button>
    </div>
    <div style={{marginTop: 20}}>
        <Button onClick={() => togglePopup('popupRight')}>Popup справа</Button>
    </div>
    <div style={{marginTop: 20}}>
        <Button onClick={() => togglePopup('popupWithoutParanja')}>Popup без паранжи</Button>
    </div>
    <div style={{marginTop: 20}}>
        <Button onClick={() => togglePopup('popupWithoutBackdropHandler')}>Popup без закрытия по клику на паранжу</Button>
    </div>

    <PopupSlider
        position='bottom'
        onClose={() => togglePopup('popupBottom')}
        hasBackdropClose={true}
        visible={state.popupBottom}
        closer={true}
    >
        <div style={{height: '400px', padding: '20px'}}>Попап снизу с закрытием</div>
    </PopupSlider>

    <PopupSlider
        position='right'
        onClose={() => togglePopup('popupRight')}
        hasBackdropClose={true}
        visible={state.popupRight}
        closer={true}
    >
        <div style={{width: '400px', padding: '20px'}}>Попап справа с закрытием</div>
    </PopupSlider>

    <PopupSlider
        position='right'
        onClose={() => togglePopup('popupWithoutParanja')}
        hasBackdrop={false}
        visible={state.popupWithoutParanja}
        closer={true}
    >
        <div style={{
            width: '400px',
            padding: '20px',
            backgroundColor: '#e3e3e3',
            height: '100%',
        }}>Попап без паранжи</div>
    </PopupSlider>

    <PopupSlider
        position='right'
        onClose={() => togglePopup('popupWithoutBackdropHandler')}
        visible={state.popupWithoutBackdropHandler}
        closer={true}
    >
        <div style={{
            width: '400px',
            padding: '20px',
        }}>Попап без закрытия по клику на паранжу</div>
    </PopupSlider>
</div>
```
