## Quotas management API (https://core-quotateka.maps.yandex.net)
API для управления квотами на использование сервисов карт.  
`Клиент` - ABC-сервис которому выданы квоты.  
`Провайдер` - ABC-сервис карт предоставляющий ресурсы для использования клиентами в рамках выданных квот.  
Квоты определены в терминах рейтлимитера, то есть количества запросов к ресурсу в интервал времени.  

"Выданная"(`dispensed`) квота - максимальное значение, разрешенное клиентскому аккаунту для аллокации.  
"Аллоцированная"(`allocated`) квота - значение, которое применяет провайдер для квотирования запросов клиента.  
Эти значения могут не совпадать, так как аллокация это отдельная операция.

Через API команды клиентов распределяют выданные квоты по аккаунтам и привязывают к примитивам межсервисной TVM аутентификации.  
Доступ на запись разрешен только команде соответствующего ABC-сервиса.  
Доступ на чтение не ограничиваем, но креденшлы в запросах проверяем.  

**Авторизация**: по креденшлам внутреннего паспорта (OAuth token / TVM2 user ticket).

**GET `/client/get?client_abc=<abc_slug>[&client_id=<client_id>&account_id=<account_id>]`**  
Получить профиль клиента по идентификатору, `abc_slug` или аккаунту.  
__Response__: proto.ClientProfile

**POST `/account/create?client_id=<client_id>&provider_id=<provider_id>&account_slug=<account_slug>&name=<string>[&description=<string>]`**  
Создать новый клиентский аккаунт.  
Параметр `account_slug` - короткий текстовый идентификатор из латинских букв, цифр, подчеркиваний и дефисов, уникальный для клиента.  
__Request__: Empty  
__Response__: proto.Account

**POST `/account/rename?account_id=<account_id>[&name=<string>&description=<string>]`**  
Изменить имя/описание аккаунта.  
__Request__: Empty  
__Response__: proto.Account

**POST `/account/dispense_quota?account_id=<account_id>`**  
Изменить выданные аккаунту квоты.  
В запросе передаются квоты, которые получат новые значения. Чтобы освободить квоту, нужно задать ей нулевой лимит.  
Запрещено устанавливать значение выданной квоты меньше аллоцированного, для этого сначала нужно изменить размер аллокации.  
Сумма квот аккаунтов не может превышать общий размер квот выданных клиенту.  
__Request__: proto.UpdateProviderQuotasRequest  
__Response__: proto.Account

**POST `/account/allocate_quota?account_id=<account_id>`**  
Изменить аллокацию квот для аккаунта. Аллоцированные значения применяет провайдер для квотирования.  
В запросе передаются аллокации, которые получат новые значения. Чтобы полностью деаллоцировать квоту, нужно задать ей нулевой лимит.  
Клиент не может аллоцировать квоту больше чем выдана аккаунту.  
**NB**: Задать аллокацию с превышением выданной квоты может обладатель роли `Администратор` в ABC соответствующего провайдера.  
__Request__: proto.UpdateProviderQuotasRequest  
__Response__: proto.Account

**POST `/account/assign_tvm?tvm_id=<tvm_id>&account_id=<account_id>&name=<name>`**  
Привязать tvm к аккаунту. Привязка нужна, чтобы провайдер применял аккаунтную квоту для запросов авторизованных этим tvm.  
Один и тот же tvm разрешено привязать к нескольким аккаунтам если их провайдеры отличаются.  
Если tvm уже привязан к этому аккаунту, то запрос изменит имя и завершится успешно.  
**NB:** Если tvm уже привязан к другому аккаунту этого провайдера, то результатом будет ошибка `409, Unique constraint violation`  
Параметр `name` - человекочитаемый алиас для tvm  
__Request__: Empty  
__Response__: proto.Account

**POST `/account/move_tvm?tvm_id=<tvm_id>&from_account_id=<account_id>&to_account_id=<account_id>`**  
Атомарно переносит tvm между аккаунтами.  
Аккаунты должны относиться к одному провайдеру и принадлежать одному клиенту.  
**NB:** Для переноса между аккаунтами разных клиентов/провайдеров нужно использовать связку `revoke_tvm`/`assign_tvm`  
__Request__: Empty  
__Response__: proto.Account

**POST `/account/revoke_tvm?tvm_id=<tvm_id>&account_id=<account_id>`**  
Отвязать tvm идентификатор от аккаунта.
__Request__: Empty  
__Response__: proto.Account


**GET `/account/get?account_id=<account_id>`**  
Получить описание аккаунта.  
__Request__: Empty  
__Response__: proto.Account

**POST `/account/close?account_id=<account_id>`**  
Закрыть аккаунт.  
Перед закрытием нужно деаллоцировать квоты - попытка закрыть аккаунт с ненулевыми аллокациями приведет к ошибке.  
Выданные квоты закрытых аккаунтов не учитываются при проверки ограничения на суммарную квоту.  
 __Request__: Empty  
__Response__: proto.Account

**POST `/account/reopen?account_id=<account_id>`**  
Переоткрыть закрытый аккаунт.  
Запрос вернет ошибку, если выданные в аккаунте квоты не укладываются в суммарную квоту клиента.  
__Request__: Empty  
__Response__: proto.Account

**GET `/client/lookup?provider_id=<provider_id>[&tvm_id=<tvm_id>]`**  
Поиск зарегистрированных клиентов по параметрам.  
Параметр `provider` - клиенты, с квотами заданного провайдера.  
Параметр `tvm` - клиента по tvm идентификатору, привязанному к его аккаунту.  
__Response__: proto.ClientsList

**GET `/account/lookup?[client_id=<client_id>&account_slug=<account_slug>&provider_id=<provider_id>&tvm_id=<tvm_id>]`**  
Поиск аккаунтов по параметрам.
Параметр `client_id` - аккаунты заданного клиента.  
Параметр `account_slug` - аккаунт с указанным слагом.  
Параметр `provider` - аккаунты заданного провайдера.  
Параметр `tvm` - аккаунт, по привязанному tvm идентификатору.  
__Request__: Empty  
__Response__: proto.AccountsList

**GET `/provider/get?provider_id=<provider_id>[provider_abc=<abc_slug>]`**  
Получить профиль провайдера по идентификатору или `abc_slug`.  
__Response__: proto.ProviderProfile 


---


## Configuration API (https://core-quotateka-server.maps.yandex.net)

#### Ручки загрузки конфигурации  
API для загрузки конфигурации провайдеров и выданных клиентам квот.  
**TODO**: синхронизаии с Dispenser.  
При авторизации доступа проверяется роль администратор в ABC quotateka.  

**Авторизация**: по креденшлам внутреннего паспорта (OAuth token / TVM2 user ticket). 

**POST `/configuration/provider_update?provider_id=<provider_id>`**  
Изменить параметры провайдера.  
Если это новый провайдер, то он автоматически регистрируется.  
__Request__: proto.UpdateProviderRequest  
__Response__: proto.ProviderProfile  

**POST `/configuration/client_update?client_abc=<abc_slug>&provider_id=<provider_id>`**  
Установить выданные клиенту квоты (выгрузка квот из аркадии).  
Новый клиент автоматически регистрируется, для него создается дефотный аккаунт в который помещается вся выданная квота.  
При обновлении клиента происходит обновление квот, при этом удалённые из конфига квоты автоматом удаляются из базы, но
только в том случае если они не используются в аккаунтах. При контроле (и удалении) используются только квоты заданного
провайдера. Если квоты используются, то всё обновление фэйлится.  
**TODO**: Для выгрузки квот из Диспенсера отдельная ручка.  
__Request__: proto.UpdateQuotasRequest  
__Response__: proto.ClientProfile

#### Ручки чтения конфигурации  

**Авторизация**: по TVM2 service-тикетам  

**GET `/provider/inventory?provider=<provider_id>`**  
Выгрузка данных ключей/аккаунтов/квот для агентов на хостах провайдера.  
**Авторизация**: service-тикет от лица tvm-приложения провайдера.  
__Response__: proto.ProviderInventory
