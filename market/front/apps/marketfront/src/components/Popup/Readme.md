
```jsx
import Button from '@self/root/src/uikit/components/Button';

initialState = {
    popup: false,
};

const togglePopup = (name) => {
    setState({[name]: !state[name]});
};

let popup;

if (state.popup === true) {
    popup = <Popup position='bottom'>Текст</Popup>;
}

const style = {marginTop: 20};

<div>
    <div style={{marginTop: 20}}>
        <Button onClick={() => togglePopup('popup')}>Popup показать</Button>
    </div>
    <div style={{marginTop: 20}}>
        <Button onClick={() => togglePopup('popup')}>Popup закрыть</Button>
    </div>

    {popup}
</div>
```
