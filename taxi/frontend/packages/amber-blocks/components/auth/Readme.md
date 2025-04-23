```jsx
const AuthModal = require('./AuthModal.styl');
const users = [
    {
        login: 'bratva-test',
        id: '3000382444',
        avatarId: '1824/3000382444-40336',
        email: 'bratva.test@yandex.ru'
    },
    {
        login: 'Дэн Абрамов',
        id: '4010776088',
        email: 'passport-test-email-long-spa-and-thai-resort-laxury@yandex.ru'
    }
];

const users2 = [
{
    login: 'bratva-test',
    id: '3000382444',
    email: 'bratva.test@yandex.ru'
},
{
    login: 'Дэн Абрамов',
    id: '4010776088',
    avatarId: '1824/3000382444-40336',
    email: 'passport-test-email-long-spa-and-thai-resort-laxury@yandex.ru'
},
{
    login: 'Кулаков',
    id: '4010776089',
    avatarId: '1824/4010776089-40336',
    email: 'passport-test'
}
];


<div>
    <p>Блок с авторизацией</p>
    <Auth/>

    <p>
        С авторизацией - мульти аккаунт.<br/>
        <em>Пользователи передаются в `users`, поля `login`, `avatarId`, `email` не используются</em>
    </p>
    <Auth 
        passportHost="https://passport-test.yandex.ru"
        userProps={{avatarHost: '//avatars.mdst.yandex.net'}}
        allowMoreUsers
        defaultUid={users[0].id}
        users={users}
    />
    
    <p>Произвольный набор пропсов</p>
    <Auth 
        passportHost="https://passport-test.yandex.ru"
        userProps={{avatarHost: '//avatars.mdst.yandex.net', maxLength: 6}}
        allowMoreUsers
        defaultUid={users2[0].id}
        yu={123123}
        retpath="//yandex.ru"
        signinText="SingIn"
        signoutText="Свалить"
        addAccountText="Хочу еще!"
        popupProps={{placement: 'top-start', children: 'ТУТ МОЙ МИР!', className: 'MyPopup'}}
        users={users2}
    />
</div>
```
