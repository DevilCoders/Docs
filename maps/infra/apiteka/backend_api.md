## Account API (https://core-apiteka.maps.yandex.net)
API для управления ключами аккаунта. Аккаунт привязан к паспортному пользователю.  
**Авторизация**: по креденшлам внешного паспорта (OAuth token / session cookie / TVM2 User-тикет)

**POST `/account/register`**  
Ручка для регистрация аккаунта. Владельцем аккаунта становится пользователь чьи креденшлы переданы в запросе.  
__Request__: Empty  
__Response__: proto.Account  

**POST `/account/accept`**  
Владелец аккаунта принимает текущую версию соглашения Terms Of Service.  
При обновлении Terms Of Service, для существующих аккаунтов нужно повторно вызвать `/account/accept`.  
__Request__: Empty  
__Response__: proto.Account  

**GET `/account/get`**  
Получить профиль своего аккаунта.  
__Response__: proto.Account

**POST `/project/create?name=<string>[&description=<string>]`**  
Создать новый проект.  
__Request__: Empty  
__Response__: proto.Project

**POST `/project/get?project=<project_id>`**  
Полное описание проекта по идентификатору.  
__Request__: Empty  
__Response__: proto.Project

**POST `/project/rename?project=<project_id>[&name=<string>&description=<string>]`**  
Изменить имя/описание проекта.  
__Request__: Empty  
__Response__: proto.Project

**POST `/project/attach_api?project=<project_id>&api_provider=<api_provider_id>[&tariff=<tariff_id>]`**  
Подключить провайдера API к проекту или сменить тариф для уже подключенного.  
Доступны только бесплатные тарифы (с аттрибутом `is_default=true`) этого API провайдера.  
Если не указать тариф в запросе, то он будет выбран автоматически.  

Подключение необходимо, чтобы API могло обслуживать запросы с ключами этого проекта.  
__Request__: Empty  
__Response__: proto.Project

**POST `/project/detach_api?project=<project_id>&api_provider=<api_provider_id>`**  
Отключить API от проекта.  
После отключения API перестанет обслуживать запросы с ключами этого проекта.  
__Request__: Empty  
__Response__: proto.Project

**POST `/project/close?project=<project_id>`**  
Закрыть проект. Все ключи закрытого проекта автоматически блокируются.  
__Request__: Empty  
__Response__: proto.Project

**POST `/project/reopen?project=<project_id>`**  
Переоткрыть закрытый проект.  
__Request__: Empty  
__Response__: proto.Project

**POST `/key/create?project=<project_id>&name=<string>`**  
Создать новый ключ в проекте.   
__Request__: Empty  
__Response__: proto.ApiKey

**POST `/key/clone?key=<api_key>`**  
Склонировать ключ.  
Клон получит уникальные значения `key` и `secret`, остальные поля будут скопированы из ключа-оригинала.      
__Request__: Empty  
__Response__: proto.ApiKey

**POST `/key/block?key=<api_key>[&expires=<timestamp>]`**  
Заблокировать ключ.  
В параметре expires можно явно задать момент когда ключ перестанет работать.  
По-умолчанию expires устанавливается в now() и ключ блокируется сразу.  
__Request__: Empty  
__Response__: proto.ApiKey

**POST `/key/unblock?key=<api_key>`**  
Разблокировать ключ.  
__Request__: Empty  
__Response__: proto.ApiKey

**POST `/key/restrict?key=<api_key>`**  
Задать restrictions ключа  
__Request__: proto.UpdateKeyRestrictionsRequest  
__Response__: proto.ApiKey

**GET `/provider/get?provider=<provider_id>`**  
Профиль провайдера по идентификатору.  
__Response__: proto.ApiProvider  

**GET `/provider/lookup[?name=<string>&tariff=<api_tariff_id>]`**  
Поиск API провайдеров по параметрам.  
__Response__: proto.ProvidersList  

---


## Admin API (https://core-apiteka-admin.maps.yandex.net)
API администратора позволяет управлять всеми аккаунтами и ключами в системе.
Администратор - пользователь из внутреннего паспорта (@yandex-team) с соответствующей ролью в ABC.

**Авторизация**: по креденшлам внутреннего паспорта (OAuth token / TVM2 User-тикет). 

**GET `/account/lookup?[provider=<provider_id>&tariff=<api_tariff_id>&owner=<login>&key=<api_key>&project=<project_id>&blocked=<bool>]`**
Поиск зарегистрированных акканутов в системе.  
Параметры поиска:
`provider` - подключенный api-провайдер
`tariff` - подключеный тариф
`owner` - владелец аккаунта 
`key` - api-ключ
`project` - идентификатор проекта
`blocked` - фильтр активных/заблокированных.  
__Response__: proto.AccountsList

**GET `/account/get?account=<account_id>`**  
Получить профиль аккаунта.  
__Response__: proto.Account

**POST `/account/block?account=<account_id>`**  
Заблокировать аккаунт.  
__Request__: Empty  
__Response__: proto.Account  

**POST `/account/unblock?account=<account_id>`**  
Разблокировать аккаунт.  
__Request__: Empty  
__Response__: proto.Account  

**POST `/account/chown?account=<account_id>&new_owner=<login>`**  
Поменять владельца аккаунта.  
__Request__: Empty  
__Response__: proto.Account  

**POST `/project/get?project=<project_id>`**  
Полное описание проекта по идентификатору.  
__Request__: Empty  
__Response__: proto.Project

**POST `/project/attach_api?project=<project_id>&api_provider=<api_provider_id>&tariff=<tariff_id>`**  
Подключить тариф на API для проекта.  
__Request__: Empty  
__Response__: proto.Project

**GET `/key/get?key=<api_key>`**  
Получить информацию о ключе.  
__Response__: proto.ApiKey

**GET `/provider/lookup[?name=<string>&tariff=<api_tariff_id>]`**  
Поиск API провайдеров по параметрам.  
__Response__: proto.ProvidersList  

**POST `/provider/update?provider=<provider_id>`**  
Добавить нового API провайдера или изменить параметры существующего.  
__Request__: proto.UpdateApiProviderRequest  
__Response__: Empty  

**POST `/provider/tariff/update?provider=<provider_id>&tariff=<tariff_id>`**  
Добавить новый тариф для API провайдера или изменить параметры существующего.  
__Request__: proto.UpdateTariffRequest  
__Response__: Empty  

**GET `/log?[key=<api_key>&project=<project_id>&author=<login>]`**  
Лог изменений ключей и проектов.  
В параметрах можно запросить конкретный ключ / проект, а также автора изменений.  
__Response__: proto.Log


---


## Service API (https://core-apiteka-server.maps.yandex.net)
Служебное апи.  
**Авторизация**: по TVM2 service-тикетам  

**GET `/provider/inventory?provider=<provider_id>`**  
Выгрузка данных ключей/проектов/квот для агентов на хостах провайдера.  
**Авторизация**: service-тикет от лица tvm-приложения провайдера.  
__Response__: proto.ProviderInventory
