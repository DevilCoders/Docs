# Интерфейс мультиавторизации

Для управления мультиавторизацией пользователю должны быть доступны следующие функции:

- Переключение основного аккаунта в куке `Session_id`.

    Реализуется вызовом режима [embeddedauth](https://beta.wiki.yandex-team.ru/passport/frontend/embeddedauth-multiauth/) с параметром `action=change_default`.

- Добавление нового аккаунта в куку `Session_id`.

    Для этого следует перенаправить пользователя на адрес [https://passport.yandex.ru/auth?mode=add-user](https://passport.yandex.ru/auth?mode=add-user) с query-параметром `retpath` (ссылка для возвращения на сервис в формате urlencode).

- Выход из основного аккаунта.

    Для этого следует перенаправить пользователя на адрес `https://passport.yandex.ru/passport?mode=logout` с query-параметром `retpath` (ссылка для возвращения на сервис в формате urlencode).

    Если в куке `Session_id` указано несколько аккаунтов, режим `logout` удаляет только основной. Новым основным аккаунтом становится следующий в списке.


Элементы интерфейса мультиавторизации реализованы в Лего в блоке [user](https://lego.yandex-team.ru/libs/islands/v3.9.0/desktop/user/#Меню-пользователя-с-мультиавторизацией-menu_multiauth) (библиотека `islands-user` версии 3.8.0).

> Визуально и в Паспорте, и в Лего интерфейс мультиавторизации скрыт в выпадающем меню пользователя в шапке:
> ![image](../../_assets/multiauth.png)

