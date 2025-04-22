Логотип

[logo in figma](https://www.figma.com/file/od4T6x5g2eMur3nKh3AinF/Yandex-Go-%7C-redesign?node-id=0%3A1)

```jsx
const RadioButton = require('../radio-button').default;
 initialState = {service: 'taxi', theme: 'normal', lang: 'ru'};

<div>
 <RadioButton
     options={[
        {label: 'taxi', value: 'taxi'},
        {label: 'go', value: 'go'},
        {label: 'go-taxi', value: 'go-taxi'}
     ]}
     onChange={(value) => {
        setState({service: value, theme: state.theme, lang: state.lang})
     }}
     name="service"
     value={state.service}
 />

 <RadioButton
     options={[
        {label: 'normal', value: 'normal'},
        {label: 'dark', value: 'dark'},
        {label: 'white', value: 'white'}
     ]}
     onChange={(value) => {
        setState({service: state.service, theme: value, lang: state.lang})
     }}
     name="theme"
     value={state.theme}
 />

 <RadioButton
     options={[
        {label: 'ru', value: 'ru'},
        {label: 'en', value: 'en'},
        {label: 'zz', value: 'zz'}
     ]}
     onChange={(value) => {
        setState({service: state.service, theme: state.theme, lang: value})
     }}
     name="lang"
     value={state.lang}
 />

    <div style={{padding: 24, backgroundColor: state.theme === 'white' ? '#333' : '#fff'}}>
        <Logo service={state.service} theme={state.theme} lang={state.lang} url="http://yandex.ru" serviceUrl="http://taxi.yandex.ru"/>
    </div>
</div>
```

Логотип такси
```jsx
<Logo service="taxi" url="http://yandex.ru" serviceUrl="http://taxi.yandex.ru"/>
```

Services
```jsx
const Grid = require('../../styleguide/components/grid/Grid').default;

<div>
    <Grid container spacing={3}>
        <Grid item size={4}>
            go<br/>
        </Grid>
        <Grid item size={4}>
            go-taxi<br/>
        </Grid>
    </Grid>
<br/><br/>
    <Grid container spacing={3} style={{backgroundColor: '#E0DEDA'}}>
        <Grid item size={4}>
            <Logo service="go"/>
        </Grid>
        <Grid item size={4}>
            <Logo service="go-taxi"/>
        </Grid>
    </Grid>
    <br/><br/>
    <Grid container spacing={3} style={{backgroundColor: '#E0DEDA'}}>
        <Grid item size={4}>
            <Logo service="go" lang="en"/>
        </Grid>
        <Grid item size={4}>
            <Logo service="go-taxi" lang="en"/>
        </Grid>
    </Grid>
    <br/><br/>
    <Grid container spacing={3} style={{backgroundColor: '#333'}}>
        <Grid item size={4}>
            <Logo service="go" theme="white"/>
        </Grid>
        <Grid item size={4}>
            <Logo service="go-taxi" theme="white"/>
        </Grid>
    </Grid>
    <br/><br/>
    <Grid container spacing={3} style={{backgroundColor: '#333'}}>
        <Grid item size={4}>
            <Logo service="go" lang="en"theme="white"/>
        </Grid>
        <Grid item size={4}>
            <Logo service="go-taxi" lang="en"theme="white"/>
        </Grid>
    </Grid>
</div>
```

