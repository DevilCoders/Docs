Шапка
```jsx
const Auth = require('../auth').default;
<Header
    logoProps={{lang: 'ru', service: 'taxi', url: 'https://yandex.ru', serviceUrl: 'https://taxi.yandex.ru'}}
    links={[
        {name: 'Стать водителем', url: '/driver', id: 'driver'},
        {name: 'Приложение', url: '/app', id: 'app'},
        {name: 'Поддержка', url: '/support', id: 'support'},
        {name: 'Бизнесу', url: '/business', id: 'business'},
        {name: 'Блог', url: '/blog', id: 'blog', active: true},
    ]}
>
</Header>
```

Шапка с авторизацией
```jsx
const Auth = require('../auth').default;
const users = [
{
    login: 'bratva-test',
    id: '3000382444',
    avatarId: '1824/3000382444-40336',
    email: 'bratva.test@yandex.ru'
}
];

<Header
    logoProps={{lang: 'ru', service: 'taxi', url: 'https://yandex.ru', serviceUrl: 'https://taxi.yandex.ru'}}
    links={[
        {name: 'Стать водителем', url: '/driver', id: 'driver'},
        {name: 'Приложение', url: '/app', id: 'app'},
        {name: 'Поддержка', url: '/support', id: 'support'},
        {name: 'Бизнесу', url: '/business', id: 'business'},
        {name: 'Блог', url: '/blog', id: 'blog', active: true},
    ]}
>
    <Auth 
        userProps={{avatarHost: '//avatars.mdst.yandex.net'}}
        allowMoreUsers
        defaultUid={users[0].id}
        yu={123123}
        retpath="//yandex.ru"
        users={users}
    />
</Header>
```

Мобильная шапка
```jsx
const Auth = require('../auth').default;
<div style={{width: '360px', height: '500px', position: 'relative'}}>
<Header
    logoProps={{lang: 'ru', service: 'taxi', url: 'https://yandex.ru', serviceUrl: 'https://taxi.yandex.ru'}}
    links={[
        {name: 'Стать водителем', url: '/driver', id: 'driver'},
        {name: 'Приложение', url: '/app', id: 'app'},
        {name: 'Поддержка', url: '/support', id: 'support'},
        {name: 'Бизнесу', url: '/business', id: 'business'},
        {name: 'Блог', url: '/blog', id: 'blog', active: true},
    ]}
    mobileContent={<div style={{ padding: "20px 16px"}}>Content</div>}
    mobile
>
    <Auth mobile/>
</Header>
</div>
```

Мобильная шапка без меню
```jsx
<div style={{width: '360px', height: '500px', position: 'relative'}}>
<Header
    showMenu={false}
    logoProps={{lang: 'ru', service: 'taxi', url: 'https://yandex.ru', serviceUrl: 'https://taxi.yandex.ru'}}
    links={[
        {name: 'Стать водителем', url: '/driver', id: 'driver'},
        {name: 'Приложение', url: '/app', id: 'app'},
        {name: 'Поддержка', url: '/support', id: 'support'},
        {name: 'Бизнесу', url: '/business', id: 'business'},
        {name: 'Блог', url: '/blog', id: 'blog', active: true},
    ]}
    mobile
>
</Header>
</div>
```
