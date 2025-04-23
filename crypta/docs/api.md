Swagger
=======

Для документации в API Крипты используется [Swagger](https://swagger.io).
Определение Swagger интерфейса доступно через [/swagger.json](https://api.crypta.yandex-team.ru/swagger.json),
а Swagger UI доступен по основному адресу [api.crypta.yandex-team.ru](https://api.crypta.yandex-team.ru).


Точки входа
===========


- Людям следует использовать [api.crypta.yandex-team.ru](https://api.crypta.yandex-team.ru),
    аутентификация происходит по cookie (Sessionid)
- Роботам следует использовать [api.crypta.yandex.net](https://api.crypta.yandex.net),
    аутентификация происходит по сертификату устройства или OAuth


Аутентификация
==============

Аутентификация осуществляется тремя способами:

- _Cookie_. Этот способ используется автоматически при использовании браузера.
    Для аутентификации используется содержимое заголовка `Cookie` (конкретнее, параметр `Session_id`).
- _OAuth_. Основной способ для аутентификации роботных пользователей из смежных сервисов.
    Проверка осуществляется через заголовок `Authorization`. В этом заголовке должно быть значение вида `OAuth <token>`.
- _Сертификат_. Аутентификация через сертификат используется в API для доступа робота IDM.

Сервис пока что не использует авторизацию через TVM.  
Получить [_OAuth_ токен](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=c92ca88b9d664402be33802f57d76dd4).

IDM
==============

Для контроля доступа к отдельным ресурсам API используется [IDM](https://idm.yandex-team.ru).
В тестовом окружении используется [тестовый IDM](https://idm.test.yandex-team.ru).

Все роли находятся в системе "Крипта".
