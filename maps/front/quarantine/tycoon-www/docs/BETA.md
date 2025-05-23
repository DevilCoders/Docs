### Беты/стенды
Примерно через полчаса после создания пул реквеста поднимается бета по адресу вида:<br/>
``
https://pr-<id пул реквеста>.beta.sprav.yandex.ru/sprav/*
``

Так же к бете можно обратиться через [crowdtest](https://wiki.yandex-team.ru/maps/dev/ui/tests/crowd/). Crowdtest позволяет обращаться к бетам из внешней сети.
Ссылка на crowdtest вида:
``
https://sprav.crowdtest.maps.yandex.ru/beta-pr-<id пул реквеста>/sprav/*
``

Для этого нужно:
1) Быть в специальной [abc-группе](https://abc.yandex-team.ru/services/maps-front-tycoon-users/).
2) Иметь yndx-* аккаунт во внешнем Яндексе. Аккаунт должен быть указан на staff. Он здесь нужен только для настройки доступа. Заходить на crowdtest можно будет и под другими пользователями.
3) Настроить для своего yandex-team [двухфакторную аутентификацию (TOTP)](https://wiki.yandex-team.ru/passport/yateamtotp/#kakvkljuchit).

#### Как зайти crowdtest бету из внешней сети:
1) Перейти по адресу https://sprav.crowdtest.maps.yandex.ru/beta-pr-<id пул реквеста>/sprav/* из внешней сети
2) При первом заходе произойдет переадресаци на passport.yandex-team.ru. Нужно ввести свои доменные (как от стафф или от ноутбука) логин и пароль.
3) Далее нужно будет ввести "Одноразовый пароль". Его можно получить в приложении Яндекс Ключ. Это как раз есть двухфакторная авторизация TOPT. Авторизация на yandex-team сохраняется в cookie. Повторять этот и предыдущий шаг нужно будет только с новых устройств.
4) После этого вы попадаете в бету. Но если у вас нет авторизации во внешнем Яндексе, то произойдет переадресация на passport.yandex.ru. Тут нужно авторизироваться под внешним пользователем. Можно и под yndx-*

Чуть более подробно процесс авторизации описан [здесь](https://st.yandex-team.ru/TYCOON-13255#61a4ca2cb401a1031868cc7a).

Ссылку на бету и на crowdtest можно найти в описании пул рекеста:<br/>
![](https://jing.yandex-team.ru/files/vsesh/uhura_2021-11-30T13%3A03%3A32.459682.jpg)
