```jsx
<div>
    <p>Пользователь</p>
    <User login="test-user"/>

    <p>Пользователь с photo</p>
    <User login="test-user" showCamera/>

    <p>Кастомный хост для аватарки</p>
    <User login="test-user" avatarId="1824/3000382444-40336" avatarHost="//avatars.mdst.yandex.net"/>

    <p>Только аватарка</p>
    <User login="test-user" showLogin={false}/>

    <p>Только логин</p>
    <User login="test-user" showAvatar={false}/>
</div>
```
