```jsx
const MobileMenu = require('./MobileMenu').default;
initialState = {showMenu: true};
<React.Fragment>
<div onClick={() => setState({ showMenu: true })}>Показать меню</div>
<MobileMenu
    links={[
        {name: 'Стать водителем', url: '/driver', id: 'driver'},
        {name: 'Приложение', url: '/app', id: 'app'},
        {name: 'Поддержка', url: '/support', id: 'support'},
        {name: 'Бизнесу', url: '/business', id: 'business'},
        {name: 'Блог', url: '/blog', id: 'blog', active: true},
    ]}
    mobileContent={<div style={{ padding: "20px 16px"}}>Кнопка</div>}
    show={state.showMenu}
    onClickOverlay={() => setState({ showMenu: false })}
    closeOnSwipe={() => setState({ showMenu: false })}
/>
</React.Fragment>
```
