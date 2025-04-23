# Пиннинг мультиавторизации

## Блэкбокс

В AuthenticationController'е при обращении в блэкбокс добавляется параметр default_uid:
https://github.yandex-team.ru/passport-frontend/lib-controllers/blob/fae2074c5e30b2301126c4a3f7265f85615e02b8/Authentication.js#L163

Этот default_uid берётся из параметра uid в запросе (гет-параметр, или из body):
https://github.yandex-team.ru/passport-frontend/lib-controllers/blob/fae2074c5e30b2301126c4a3f7265f85615e02b8/Authentication.js#L51

Включается-выключается через метод togglePinning (по-дефолту выключено):
https://github.yandex-team.ru/passport-frontend/lib-controllers/blob/fae2074c5e30b2301126c4a3f7265f85615e02b8/Authentication.js#L98-L101

В паспорте за включение пиннинга отвечает флаг multiauthPinning в конфиге.
Вот так передаётся в AuthController:
https://github.yandex-team.ru/passport-frontend/passport/blob/rc-0.2.20/lib/controller/index.js#L81


## Лэйаут

На клиент знание об уиде передаётся через лэйаут.
Вот вьюха, которая генерит данные для яти:
https://github.yandex-team.ru/passport-frontend/passport/blob/ad2f914561308205690a1717b649c8bd34f62f15/blocks/layout/RenderingLayoutView.js#L63-L85

Вот эти данные в яти:
https://github.yandex-team.ru/passport-frontend/passport/blob/ad2f914561308205690a1717b649c8bd34f62f15/blocks/layout/layout.yate#L88-L92

Это /глобальные/ переменные в джаваскрипте.


## Переключение дефолта в куке

За отслеживание статуса вкладки и переключение дефолта отвечает вот этот кусок:
https://github.yandex-team.ru/passport-frontend/passport/blob/ad2f914561308205690a1717b649c8bd34f62f15/blocks/MaChangedefault.js

Сценарий:
Когда вкладка становится активной,
проверяем изменился ли yandex_login.
Если изменился, то возвращаем дефолт как был.
 

## Пиннинг

В passport.request.api дописываем уид. Таким образом большинство аяксовых запросов начинают содержать уид:
https://github.yandex-team.ru/passport-frontend/passport/blob/ad2f914561308205690a1717b649c8bd34f62f15/blocks/blocks.js#L21-L24

В урл добавляем уид, чтобы правильно работала перезагрузка по f5, восстановление вкладки и т.д.
https://github.yandex-team.ru/passport-frontend/passport/blob/ad2f914561308205690a1717b649c8bd34f62f15/blocks/blocks.js#L26-L39
