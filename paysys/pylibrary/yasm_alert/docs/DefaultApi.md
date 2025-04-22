# yasm_alert.DefaultApi

All URIs are relative to *https://yasm.yandex-team.ru/srvambry/alerts*

Method | HTTP request | Description
------------- | ------------- | -------------
[**bind_check**](DefaultApi.md#bind_check) | **POST** /bind_check | Bind yasm alert to juggler check
[**create_alert**](DefaultApi.md#create_alert) | **POST** /create | Create new alert
[**delete_alert**](DefaultApi.md#delete_alert) | **POST** /delete | Delete one alert
[**get_alert**](DefaultApi.md#get_alert) | **GET** /get | Get one alert
[**list_alerts**](DefaultApi.md#list_alerts) | **GET** /list | Get checks by filter
[**replace_alerts**](DefaultApi.md#replace_alerts) | **POST** /replace | Replace alerts with prefix
[**unbind_check**](DefaultApi.md#unbind_check) | **POST** /unbind_check | Remove binding between yasm alert and juggler check
[**update_alert**](DefaultApi.md#update_alert) | **POST** /update | Update one alert


# **bind_check**
> bind_check(alert_name, check_host, check_service)

Bind yasm alert to juggler check

### Example
```python
from __future__ import print_function
import time
import yasm_alert
from yasm_alert.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = yasm_alert.DefaultApi()
alert_name = 'alert_name_example' # str | 
check_host = 'check_host_example' # str | 
check_service = 'check_service_example' # str | 

try:
    # Bind yasm alert to juggler check
    api_instance.bind_check(alert_name, check_host, check_service)
except ApiException as e:
    print("Exception when calling DefaultApi->bind_check: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **alert_name** | **str**|  | 
 **check_host** | **str**|  | 
 **check_service** | **str**|  | 

### Return type

void (empty response body)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **create_alert**
> InlineResponse2002 create_alert(body)

Create new alert

### Example
```python
from __future__ import print_function
import time
import yasm_alert
from yasm_alert.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = yasm_alert.DefaultApi()
body = yasm_alert.Alert() # Alert | Alert object to be created

try:
    # Create new alert
    api_response = api_instance.create_alert(body)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling DefaultApi->create_alert: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**Alert**](Alert.md)| Alert object to be created | 

### Return type

[**InlineResponse2002**](InlineResponse2002.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **delete_alert**
> delete_alert(name)

Delete one alert

### Example
```python
from __future__ import print_function
import time
import yasm_alert
from yasm_alert.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = yasm_alert.DefaultApi()
name = 'name_example' # str | Name of check to delete

try:
    # Delete one alert
    api_instance.delete_alert(name)
except ApiException as e:
    print("Exception when calling DefaultApi->delete_alert: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **name** | **str**| Name of check to delete | 

### Return type

void (empty response body)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_alert**
> InlineResponse200 get_alert(name, with_checks=with_checks)

Get one alert

### Example
```python
from __future__ import print_function
import time
import yasm_alert
from yasm_alert.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = yasm_alert.DefaultApi()
name = 'name_example' # str | Name of check to get
with_checks = 'with_checks_example' # str | Include juggler checks (optional) (optional)

try:
    # Get one alert
    api_response = api_instance.get_alert(name, with_checks=with_checks)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling DefaultApi->get_alert: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **name** | **str**| Name of check to get | 
 **with_checks** | **str**| Include juggler checks (optional) | [optional] 

### Return type

[**InlineResponse200**](InlineResponse200.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **list_alerts**
> InlineResponse2001 list_alerts(hosts=hosts, signal_pattern=signal_pattern, name_pattern=name_pattern, name_prefix=name_prefix, name=name, limit=limit, offset=offset, sorted=sorted, with_checks=with_checks)

Get checks by filter

### Example
```python
from __future__ import print_function
import time
import yasm_alert
from yasm_alert.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = yasm_alert.DefaultApi()
hosts = 'hosts_example' # str | значение имя группы или метагруппы для алерта или несколько допустимых значений через запятую (optional)
signal_pattern = 'signal_pattern_example' # str | регулярное выражение по которому будут сматчены сигналы алертов (optional)
name_pattern = 'name_pattern_example' # str | регулярное выражение по которому будут сматчены имена алертов (optional)
name_prefix = 'name_prefix_example' # str | показать алерты только с заданным префиксом (optional)
name = 'name_example' # str | имя конкретного алерта (optional)
limit = 'limit_example' # str | сколько алертов вернуть в выдаче (optional)
offset = 'offset_example' # str | сколько алертов пропустить перед началом выдачи (optional)
sorted = 'sorted_example' # str | направление сортировки (asc, desc), сортировка производится по имени алерта (optional)
with_checks = 'with_checks_example' # str | если равно true, то к алертам, провязанным с проверками Джаглера (поле  juggler_check ), будет добавлено описание этих проверок. Если аргумент with_checks не равен true, то будут показаны только host и service соответствующей проверок (optional)

try:
    # Get checks by filter
    api_response = api_instance.list_alerts(hosts=hosts, signal_pattern=signal_pattern, name_pattern=name_pattern, name_prefix=name_prefix, name=name, limit=limit, offset=offset, sorted=sorted, with_checks=with_checks)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling DefaultApi->list_alerts: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **hosts** | **str**| значение имя группы или метагруппы для алерта или несколько допустимых значений через запятую | [optional] 
 **signal_pattern** | **str**| регулярное выражение по которому будут сматчены сигналы алертов | [optional] 
 **name_pattern** | **str**| регулярное выражение по которому будут сматчены имена алертов | [optional] 
 **name_prefix** | **str**| показать алерты только с заданным префиксом | [optional] 
 **name** | **str**| имя конкретного алерта | [optional] 
 **limit** | **str**| сколько алертов вернуть в выдаче | [optional] 
 **offset** | **str**| сколько алертов пропустить перед началом выдачи | [optional] 
 **sorted** | **str**| направление сортировки (asc, desc), сортировка производится по имени алерта | [optional] 
 **with_checks** | **str**| если равно true, то к алертам, провязанным с проверками Джаглера (поле  juggler_check ), будет добавлено описание этих проверок. Если аргумент with_checks не равен true, то будут показаны только host и service соответствующей проверок | [optional] 

### Return type

[**InlineResponse2001**](InlineResponse2001.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **replace_alerts**
> replace_alerts(body)

Replace alerts with prefix

### Example
```python
from __future__ import print_function
import time
import yasm_alert
from yasm_alert.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = yasm_alert.DefaultApi()
body = yasm_alert.Body() # Body | Обновление пачки алертов - принимает список новых алертов и префикс. Удаляет все алерты с этим префиксом и сохраняет новые алерты, начинающиеся с \"<префикс>.\". Подходит для генераторов, полностью перегенерирующих набор своих алертов. Например Quentao использует префикс gen. 

try:
    # Replace alerts with prefix
    api_instance.replace_alerts(body)
except ApiException as e:
    print("Exception when calling DefaultApi->replace_alerts: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**Body**](Body.md)| Обновление пачки алертов - принимает список новых алертов и префикс. Удаляет все алерты с этим префиксом и сохраняет новые алерты, начинающиеся с \&quot;&lt;префикс&gt;.\&quot;. Подходит для генераторов, полностью перегенерирующих набор своих алертов. Например Quentao использует префикс gen.  | 

### Return type

void (empty response body)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **unbind_check**
> unbind_check(alert_name)

Remove binding between yasm alert and juggler check

### Example
```python
from __future__ import print_function
import time
import yasm_alert
from yasm_alert.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = yasm_alert.DefaultApi()
alert_name = 'alert_name_example' # str | 

try:
    # Remove binding between yasm alert and juggler check
    api_instance.unbind_check(alert_name)
except ApiException as e:
    print("Exception when calling DefaultApi->unbind_check: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **alert_name** | **str**|  | 

### Return type

void (empty response body)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **update_alert**
> InlineResponse200 update_alert(name, body)

Update one alert

### Example
```python
from __future__ import print_function
import time
import yasm_alert
from yasm_alert.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = yasm_alert.DefaultApi()
name = 'name_example' # str | Name of check to update
body = yasm_alert.Alert() # Alert | Updated alert object

try:
    # Update one alert
    api_response = api_instance.update_alert(name, body)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling DefaultApi->update_alert: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **name** | **str**| Name of check to update | 
 **body** | [**Alert**](Alert.md)| Updated alert object | 

### Return type

[**InlineResponse200**](InlineResponse200.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

