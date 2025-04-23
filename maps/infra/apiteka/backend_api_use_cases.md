## Роль: Владелец аккаунта в системе

Владельцем аккаунта является пользователь внешнего паспорта (yandex.ru). 
При помощи методов Account API бэкенда, владелец управляет ключами своего аккаунта.   
В системе разрешен только один аккаунт для пользователя.  

---

### Регистрация
Пользователь регистрирует аккаунт явным вызовом метода `/accounts/register`.  
Запросы в API бэкенда от пользователей без аккаунта приводят к ошибке.  

Запрос регистрации:
```python 
account_auth = {'X-Ya-User-Ticket', issue_user_ticket()}

http_response = http_get('apiteka/account/register', headers = account_auth))
new_account = apiteka_pb2.Account()
new_account.ParseFromString(http_response.content)
```

---

### Принятие Terms Of Service
Текущая версия соглашения Terms Of Service, глобальная для всей системы и задается в конфигурации в Аркадии.  
Соглашение нужно принять явно позвав ручку `/accounts/accept`.  
При изменении версии соглашения, на UI Кабинета ложится задача дать пользователю ознакомится с текстом нового соглашения и принять его.  
Запросы от имени аккаунта, не принявшего соглашение, приводят к HTTP 422 и `ErrorResponse` в теле ответа.  
Все ключи аккаунта не принявшего соглашение продолжают действовать.   

```python 
account_auth = {'X-Ya-User-Ticket', issue_user_ticket()}

http_response = http_get('apiteka/account/get', headers = account_auth))
if http_response.status_code == 422:
    response = apiteka_pb2.ErrorResponse()
    response.ParseFromString(http_response.content)
    if response.HasField('tos_not_accepted'):
        # Show current TOS agreement accept/decline?
        if showTOSpage().status != accepted:
            raise Exception('')
        # Accept TOS
        http_response = http_post("apiteka/account/accept", headers = account_auth)

account = apiteka_pb2.Account()
account.ParseFromString(http_response.content)
```

---

### Посмотреть свои проекты и ключи
В профиле аккаунта перечислены проекты. 
К проектам привязаны ключи для доступа к API.

Запросы в бэкенд apiteka:
```python 
account_auth = {'X-Ya-User-Ticket', issue_user_ticket()}

http_response = http_get('apiteka/account/get', headers = account_auth))
account = apiteka_pb2.Account()
account.ParseFromString(http_response.content)
# Query each project details
for project_info in account.projects:
  http_response = http_get(f'apiteka/project/get?project={project_info.id}', headers = account_auth))
  project = apiteka_pb2.Project()
  project.ParseFromString(http_response.content)
  # Keys are in project.keys collection
```

---

### Новый проект и новый ключ
Владелец аккаунта может самостоятельно создавать проекты и ключи для них.  

Запросы в бэкенд apiteka:
```python
# Create new project
http_response = http_post('apiteka/project/create', params={'name': 'my-first-project'}, 
                        headers = account_auth)
new_project = apiteka_pb2.Project()
project.ParseFromString(http_response.content)
# Create new key for the project
http_response = http_post('apiteka/key/create', params={'name': 'my-first-key', 'project': new_project.id}, 
                        headers = account_auth)
new_key = apiteka_pb2.ApiKey()
new_key.ParseFromString(http_response.content)
```

---

### Подключить API 
Чтобы использовать ключи проекта для запросов в API, необходимо подключить проект к соответствующему провайдеру.  
При подключении выдается бесплатный тариф (ограниченный) на использование этого API.  
Тарифом устанавлена квота на количество запросов за интервал времени. Квота общая для ключей проекта. 

Запросы в бэкенд apiteka:
```python
staticapi_abc = 'maps-core-renderer-staticapi'

# Select api provider from list of available
http_response = http_get('apiteka/provider/lookup', headers = account_auth)
providers = apiteka_pb2.ProvidersList()
providers.ParseFromString(http_response.content)
static_api = next(api for api in response.api_providers if api.abc_slug == staticapi_abc)

# Select project
http_response = http_get('apiteka/account/get', headers = account_auth))
account = apiteka_pb2.Account()
account.ParseFromString(http_response.content)
selected_project = next(proj for proj in account.projects if proj.name == 'my-super-project')

# Request access to selected api (tariff selected automatically)
http_response = http_post('apiteka/project/attach_api', 
                          params={'project': selected_project.id, 'api_provider': static_api.id}
                          headers = account_auth)
result_project = apiteka_pb2.Project()
result_project.ParseFromString(http_response.content)
```

---

### Отключить API 
После отключения проекта от провайдера API, его ключи нельзя использовать для запросов в это API.

Запросы в бэкенд apiteka:
```python
http_response = http_post('apiteka/project/detach_api', 
                          params={'project': selected_project.id, 'api_provider': static_api.id},
                          headers = account_auth)
# Project content in response
project = apiteka_pb2.Project()
project.ParseFromString(http_response.content)
```

---

### Подключить платный тариф на API.
Самостоятельно владелец может выбирать только бесплатные тарифы для API.  
Чтобы перевести ключ с бесплатного базового тарифа на коммерческий, владелец аккаунта оправляет заявку в B2B.  
B2B оформляют все юридически и делегируют запрос тому кто обладает ролью управляющего для этого API в нашей системе.

---

### Защитить ключ от несанкционированного использования
Владелец накладывает на ключ ограничения на использование.
Типы ограничений предопределены в системе: 
- Проверка подписи URL с ключом
- HTTP referer
- IP whitelist
- AppId приложения

Для каждого API установлены типы ограничений, которые будут проверяться для запросов с ключом.

Запросы в бэкенд apiteka:
```python
selected_key = '1530b4f6-f474-480d-b1eb-6549dcde9980'

request = apiteka_pb2.UpdateKeyRestrictionsRequest()
request.restrictions.add().signature = True
request.restrictions.add().http_referer = 'my.project.com'

http_response = http_post(f'apiteka/key/restrict?key={selected_key}', headers = account_auth,
                          data = request.SerializeToString())
result_key = apiteka_pb2.ApiKey()
result_key.ParseFromString(http_response.content)
```

---

### Заблокировать/разблокировать ключ
Владелец аккаунта может самостоятельно блокировать свои ключи.

Запросы в бэкенд apiteka:
```python
selected_key = '1530b4f6-f474-480d-b1eb-6549dcde9980'

http_response = http_post(f'apiteka/key/block?key={selected_key}', headers = account_auth)
# Key full content in response
result_key = apiteka_pb2.ApiKey()
result_key.ParseFromString(http_response.content)
```

---

### Перевыпустить скомпрометированный ключ
Можно создать новый ключ, скопировав параметры старого: проект, restriction и др.  
После чего старый ключ можно заблокировать вручную или задать дедлайн для автоматической блокировки.

Запросы в бэкенд apiteka:
```python
compromised_key = '1530b4f6-f474-480d-b1eb-6549dcde9980'
                         
# Copy compromised key parameters to a new key
http_response = http_post(f'apiteka/key/clone?key={compromised_key}', headers = account_auth)
new_key = apiteka_pb2.ApiKey() 
new_key.ParseFromString(http_response.content)

# Set compromised key expiration in 24h
http_response = http_post('apiteka/key/block',
                          params={'key': compromised_key, 'expires': now() + datetime.timedelta(hours=24)}
                          headers=account_auth)
old_key = apiteka_pb2.ApiKey()
old_key.ParseFromString(http_response.content)
```

---


## Роль: Управляющий API провайдера
Роль управляющего для конкретного API провайдера выдается в соответствующего ABC сервиса.  
Управляющий авторизуется креденшлом внутреннего паспорта (yandex-team.ru).

---

### Добавить новый тариф для API / Заморозить старый
Изменения в тарифах API, делаются через конфиг для этого API в Аркадии.  
Апдейт подхватывается CI и применяется запросом в бэкенд apiteka.
[Подробнее в кейсе про добавление API](#add-or-update-api)  

---

### Установить владельца ключа
По ключу можно найти аккаунт владельца.  

```python
http_response = http_get(f'admin.apiteka/account/lookup?key={api_key}', 
                         headers = admin_auth))
response = apiteka_pb2.AccountsList()
response.ParseFromString(http_response.content)
# Expect single entry in the result accounts collection
if response.accounts:
    owner = response.accounts[0].owner
```

---

### Выдать расширенный тариф на API
По запросу, управляющий API провайдера может установить для проекта аккаунта расширенный тариф на доступ (например коммерческий или специальный для внутренних яндексовых клиентов) через UI админки.  
Тариф выбирается из перечня доступных для данного API провайдера.  

Ниже пример когда нам известен ключ, и чтобы поменять поменять тариф сначала находим соответствующий проект.  
Запросы в бэкенд apiteka:
```python
admin_auth = {'Authorization', f'OAuth {oauth_token}'}

api_key = '1530b4f6-f474-480d-b1eb-6549dcde9980'
# Find accound by key
http_response = http_get(f'admin.apiteka/account/lookup?key={api_key}', 
                         headers = admin_auth))
response = apiteka_pb2.AccountsList()
response.ParseFromString(http_response.content)
account_info = response.accounts[0]  # Expect single entry in the response
# Get full account profile
http_response = http_get(f'admin.apiteka/account/gey?account={account_info.id}', 
                         headers = admin_auth))
account = apiteka_pb2.Account()
response.ParseFromString(http_response.content)
# New select account project by key
project = next(proj for proj in account.projects if api_key in proj.keys)

# Change tariff for project 
api_provider = 'static-api'
api_tariff = 'commercial-big'
http_response = http_post('admin.apiteka/project/attach_api', 
                          params={'project': project.id, 'api_provider': api_provider, 'tariff': api_tariff}
                          headers=admin_auth)
updated_project = apiteka_pb2.Project()
updated_project.ParseFromString(http_response.content)
```

---


## Роль: Администратор
Роль администратора выдается в ABC apiteka.

---

### Добавить API, изменить параметры API (например перечень тарифов)<a name="add-or-update-api"></a>
Кофигурация всех API провайдеров задается в аркадии. Все изменения - через ревью.  
По коммиту CI запускает таску, которая применяет изменения.

Пример конфига (maps/config/apiteka/static-api/stable.yaml):
```yaml
id: maps-static-api
abc: maps-core-renderer-staticapi
name: Static API Карт
description: 'Static API позволяет получить изображение нужного фрагмента карты, 
которое можно разместить на сайте или в приложении'
allowed_restrictions:
    - signature
    - http_referer
    - ip_address
tariffs:
    - freemium:
        default: true
        deprecated: false
        description: 'Тариф для бесплатных клиентов'
    - commercial:
        deprecated: false
        description: 'Тариф для коммерческих клиентов'
    - yandex-small:
        deprecated: false
        description: 'Тариф для маленьких внутренних клиентов'
    - yandex-big:
        deprecated: false
        description: 'Тариф для больших внутренних клиентов'
```
**TODO**: В дальнейшем планируем управление тарифами сделать через UI админки.

---

### Запретить новые ключи для устаревшего API
Для API, признанных устаревшими, можно запретить подключение новых ключей.  
Сделать это можно в конфиге API, задав аттрибут deprecated для всех default тарифов.

---

### Добавить аккаунт вручную
Администратор может завести новый аккаунт для пользователя без его участия.  
Это актуально на начальном этапе, когда будем переводить внутренних клиентов Static-API на apiteka (UI на этот момент не планируем).  

В этом сценарии, нужно создать аккаунт для временной учетки и затем сменить владельца на настоящую учетку. 

---

### Заблокировать/Разблокировать аккаунт
При блокировке аккаунта, запросы с его ключами перестают обслуживаться API провайдерами.

Запросы в бэкенд apiteka:
```python
account_owner = 'john.doe@yandex.ru'
# Find account by owner
http_response = http_get(f'admin.apiteka/account/lookup?owner={account_owner}', 
                         headers = admin_auth)
response = apiteka_pb2.AccountsList()
response.ParseFromString(http_response.content)
# Expect single account in the response
account_info = response.accounts[0]

# Block account by id
http_response = http_post(f'admin.apiteka/account/block?account={account_info.id}',
                        headers = admin_auth)
account = apiteka_pb2.Account()
account.ParseFromString(http_response.content)
```

---

### Сменить владельца аккаунта
При необходимости можно привязать аккаунт к другой учетке.

Запросы в бэкенд apiteka:
```python
old_owner = 'john.doe@yandex.ru'
new_owner = 'jane.doe@yandex.ru'
# Find it by old owner
http_response = http_get(f'admin.apiteka/account/lookup?owner={old_owner}', 
                         headers = admin_auth)
response = apiteka_pb2.AccountsList()
response.ParseFromString(http_response.content)
# Expect single account in the response
account_info = response.account[0]
# Replace onwer
http_response = http_post('admin.apiteka/account/chown', 
                          params={'account': account_info.id, 'new_owner': new_owner},
                          headers = admin_auth)
result_account = apiteka_pb2.Account()
result_account.ParseFromString(http_response.content)
```

---

### История изменений ключей/проектов
При необходимости можно запросить историю изменения ключей/проектов (в том числе привязки к API, изменения тарифа, блокировки и др).


Запросы в бэкенд apiteka:
```python
api_key = '1530b4f6-f474-480d-b1eb-6549dcde9980'

http_response = http_get(f'admin.apiteka/log?key={api_key}', 
                         headers = admin_auth)
log_response = apiteka_pb2.Log()
log_response.ParseFromString(http_response.content)
history = response.entries
```
