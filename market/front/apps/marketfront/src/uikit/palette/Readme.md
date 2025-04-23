### Цвета синего маркета

```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));

<Provider store={store}>
    <div style={{display: 'flex', flexWrap: 'wrap'}}>
        <div>
            <Palette color="gray800"/>
            <Palette color="gray700"/>
            <Palette color="gray600"/>
            <Palette color="gray500"/>
            <Palette color="gray400"/>
            <Palette color="gray300"/>
            <Palette color="gray200"/>
        </div>
        <div>
            <Palette color="purple800"/>
            <Palette color="purple600"/>
            <Palette color="blue"/>
        </div>
        <div>
            <Palette color="red600"/>
            <Palette color="red400"/>
            <Palette color="rubyRed"/>
        </div>
        <div>
            <Palette color="green600"/>
            <Palette color="green400"/>
        </div>
        <div>
            <Palette color="orange600"/>
            <Palette color="orange200"/>
        </div>
        <div>
            <Palette color="yellow400"/>
            <Palette color="yellow"/>
        </div>
        <div>
            <Palette color="white"/>
            <Palette color="iconDark"/>
            <Palette color="coalBlack"/>
            <Palette color="black"/>
        </div>
        <div>
            <Palette color="badgeOrange"/>
        </div>
    </div>
</Provider>
```
