# solomon_client.AlertingApi

All URIs are relative to *//solomon.yandex-team.ru/*

Method | HTTP request | Description
------------- | ------------- | -------------
[**create_alert_using_post**](AlertingApi.md#create_alert_using_post) | **POST** /api/v2/projects/{projectId}/alerts | Create new alert
[**create_notification_using_post**](AlertingApi.md#create_notification_using_post) | **POST** /api/v2/projects/{projectId}/notificationChannels | Create new notification channel
[**delete_alert_using_delete**](AlertingApi.md#delete_alert_using_delete) | **DELETE** /api/v2/projects/{projectId}/alerts/{alertId} | Delete alert
[**delete_notification_using_delete**](AlertingApi.md#delete_notification_using_delete) | **DELETE** /api/v2/projects/{projectId}/notificationChannels/{notificationChannelId} | Delete notification
[**explain_evaluation_sub_alert_using_get**](AlertingApi.md#explain_evaluation_sub_alert_using_get) | **GET** /api/v2/projects/{projectId}/alerts/{parentId}/subAlerts/{alertId}/explainEvaluation | Explain evaluation for exist sub alert
[**explain_evaluation_using_get**](AlertingApi.md#explain_evaluation_using_get) | **GET** /api/v2/projects/{projectId}/alerts/{alertId}/explainEvaluation | Explain evaluation for exist alert
[**explain_evaluation_using_post**](AlertingApi.md#explain_evaluation_using_post) | **POST** /api/v2/projects/{projectId}/alerts/explainEvaluation | Explain alert evaluation
[**explain_evaluation_using_post1**](AlertingApi.md#explain_evaluation_using_post1) | **POST** /api/v2/projects/{projectId}/alerts/subAlerts/explainEvaluation | Explain sub-alert evaluation
[**get_alert_evaluation_state_using_get**](AlertingApi.md#get_alert_evaluation_state_using_get) | **GET** /api/v2/projects/{projectId}/alerts/{alertId}/state/evaluation | Get alert evaluation state by id
[**get_alert_notification_state_using_get**](AlertingApi.md#get_alert_notification_state_using_get) | **GET** /api/v2/projects/{projectId}/alerts/{alertId}/state/notification | Get alert notification state by id
[**get_alert_notification_stats_using_get**](AlertingApi.md#get_alert_notification_stats_using_get) | **GET** /api/v2/projects/{projectId}/alerts/{alertId}/state/notificationStats | Get alert notification stats by id
[**get_alert_using_get**](AlertingApi.md#get_alert_using_get) | **GET** /api/v2/projects/{projectId}/alerts/{alertId} | Get alert by id
[**get_multi_alert_evaluation_state_using_get**](AlertingApi.md#get_multi_alert_evaluation_state_using_get) | **GET** /api/v2/projects/{projectId}/alerts/{alertId}/state/evaluationStats | Get alert evaluation stats by id
[**get_notification_using_get**](AlertingApi.md#get_notification_using_get) | **GET** /api/v2/projects/{projectId}/notificationChannels/{notificationChannelId} | Get notification channel by id
[**get_project_stats_using_get**](AlertingApi.md#get_project_stats_using_get) | **GET** /api/v2/projects/{projectId}/alerts/stats | Get project stats
[**get_sub_alert_evaluation_state_using_get**](AlertingApi.md#get_sub_alert_evaluation_state_using_get) | **GET** /api/v2/projects/{projectId}/alerts/{parentId}/subAlerts/{alertId}/state/evaluation | Get sub alert evaluation state by id
[**get_sub_alert_notification_state_using_get**](AlertingApi.md#get_sub_alert_notification_state_using_get) | **GET** /api/v2/projects/{projectId}/alerts/{parentId}/subAlerts/{alertId}/state/notification | Get sub alert notification state by id
[**get_sub_alert_using_get**](AlertingApi.md#get_sub_alert_using_get) | **GET** /api/v2/projects/{projectId}/alerts/{parentId}/subAlerts/{alertId} | Get sub alert by id
[**get_telegram_group_titles_using_get**](AlertingApi.md#get_telegram_group_titles_using_get) | **GET** /api/v2/telegram/groupTitles | Get telegram group titles
[**get_ya_chats_groups_using_get**](AlertingApi.md#get_ya_chats_groups_using_get) | **GET** /api/v2/yaChats/groups | Get Yandex Chats group titles and description
[**list_alerts_by_parent_using_get**](AlertingApi.md#list_alerts_by_parent_using_get) | **GET** /api/v2/projects/{projectId}/alerts/{parentId}/subAlerts | List sub alerts
[**list_alerts_by_project_using_get**](AlertingApi.md#list_alerts_by_project_using_get) | **GET** /api/v2/projects/{projectId}/alerts | List alerts
[**list_notification_using_get**](AlertingApi.md#list_notification_using_get) | **GET** /api/v2/projects/{projectId}/notificationChannels | List notification channels
[**update_alert_using_put**](AlertingApi.md#update_alert_using_put) | **PUT** /api/v2/projects/{projectId}/alerts/{alertId} | Update alert by id
[**update_notification_using_put**](AlertingApi.md#update_notification_using_put) | **PUT** /api/v2/projects/{projectId}/notificationChannels/{notificationChannelId} | Update notification channel by id

# **create_alert_using_post**
> Alert create_alert_using_post(body, project_id)

Create new alert

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.AlertingApi()
body = solomon_client.Alert() # Alert | alert
project_id = 'project_id_example' # str | projectId

try:
    # Create new alert
    api_response = api_instance.create_alert_using_post(body, project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling AlertingApi->create_alert_using_post: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**Alert**](Alert.md)| alert | 
 **project_id** | **str**| projectId | 

### Return type

[**Alert**](Alert.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **create_notification_using_post**
> NotificationChannel create_notification_using_post(body, project_id)

Create new notification channel

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.AlertingApi()
body = solomon_client.NotificationChannel() # NotificationChannel | notification
project_id = 'project_id_example' # str | projectId

try:
    # Create new notification channel
    api_response = api_instance.create_notification_using_post(body, project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling AlertingApi->create_notification_using_post: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**NotificationChannel**](NotificationChannel.md)| notification | 
 **project_id** | **str**| projectId | 

### Return type

[**NotificationChannel**](NotificationChannel.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **delete_alert_using_delete**
> delete_alert_using_delete(alert_id, project_id)

Delete alert

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.AlertingApi()
alert_id = 'alert_id_example' # str | alertId
project_id = 'project_id_example' # str | projectId

try:
    # Delete alert
    api_instance.delete_alert_using_delete(alert_id, project_id)
except ApiException as e:
    print("Exception when calling AlertingApi->delete_alert_using_delete: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **alert_id** | **str**| alertId | 
 **project_id** | **str**| projectId | 

### Return type

void (empty response body)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **delete_notification_using_delete**
> delete_notification_using_delete(notification_channel_id, project_id)

Delete notification

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.AlertingApi()
notification_channel_id = 'notification_channel_id_example' # str | notificationChannelId
project_id = 'project_id_example' # str | projectId

try:
    # Delete notification
    api_instance.delete_notification_using_delete(notification_channel_id, project_id)
except ApiException as e:
    print("Exception when calling AlertingApi->delete_notification_using_delete: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **notification_channel_id** | **str**| notificationChannelId | 
 **project_id** | **str**| projectId | 

### Return type

void (empty response body)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **explain_evaluation_sub_alert_using_get**
> AlertExplainEvaluation explain_evaluation_sub_alert_using_get(alert_id, parent_id, project_id, time=time)

Explain evaluation for exist sub alert

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.AlertingApi()
alert_id = 'alert_id_example' # str | alertId
parent_id = 'parent_id_example' # str | parentId
project_id = 'project_id_example' # str | projectId
time = 'time_example' # str | time (optional)

try:
    # Explain evaluation for exist sub alert
    api_response = api_instance.explain_evaluation_sub_alert_using_get(alert_id, parent_id, project_id, time=time)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling AlertingApi->explain_evaluation_sub_alert_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **alert_id** | **str**| alertId | 
 **parent_id** | **str**| parentId | 
 **project_id** | **str**| projectId | 
 **time** | **str**| time | [optional] 

### Return type

[**AlertExplainEvaluation**](AlertExplainEvaluation.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **explain_evaluation_using_get**
> AlertExplainEvaluation explain_evaluation_using_get(alert_id, project_id, time=time)

Explain evaluation for exist alert

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.AlertingApi()
alert_id = 'alert_id_example' # str | alertId
project_id = 'project_id_example' # str | projectId
time = 'time_example' # str | time (optional)

try:
    # Explain evaluation for exist alert
    api_response = api_instance.explain_evaluation_using_get(alert_id, project_id, time=time)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling AlertingApi->explain_evaluation_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **alert_id** | **str**| alertId | 
 **project_id** | **str**| projectId | 
 **time** | **str**| time | [optional] 

### Return type

[**AlertExplainEvaluation**](AlertExplainEvaluation.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **explain_evaluation_using_post**
> AlertExplainEvaluation explain_evaluation_using_post(body, project_id, time=time)

Explain alert evaluation

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.AlertingApi()
body = solomon_client.Alert() # Alert | alert
project_id = 'project_id_example' # str | projectId
time = 'time_example' # str | time (optional)

try:
    # Explain alert evaluation
    api_response = api_instance.explain_evaluation_using_post(body, project_id, time=time)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling AlertingApi->explain_evaluation_using_post: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**Alert**](Alert.md)| alert | 
 **project_id** | **str**| projectId | 
 **time** | **str**| time | [optional] 

### Return type

[**AlertExplainEvaluation**](AlertExplainEvaluation.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **explain_evaluation_using_post1**
> AlertExplainEvaluation explain_evaluation_using_post1(body, project_id, time=time)

Explain sub-alert evaluation

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.AlertingApi()
body = solomon_client.SubAlert() # SubAlert | subAlert
project_id = 'project_id_example' # str | projectId
time = 'time_example' # str | time (optional)

try:
    # Explain sub-alert evaluation
    api_response = api_instance.explain_evaluation_using_post1(body, project_id, time=time)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling AlertingApi->explain_evaluation_using_post1: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**SubAlert**](SubAlert.md)| subAlert | 
 **project_id** | **str**| projectId | 
 **time** | **str**| time | [optional] 

### Return type

[**AlertExplainEvaluation**](AlertExplainEvaluation.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_alert_evaluation_state_using_get**
> AlertEvaluationState get_alert_evaluation_state_using_get(alert_id, project_id)

Get alert evaluation state by id

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.AlertingApi()
alert_id = 'alert_id_example' # str | alertId
project_id = 'project_id_example' # str | projectId

try:
    # Get alert evaluation state by id
    api_response = api_instance.get_alert_evaluation_state_using_get(alert_id, project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling AlertingApi->get_alert_evaluation_state_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **alert_id** | **str**| alertId | 
 **project_id** | **str**| projectId | 

### Return type

[**AlertEvaluationState**](AlertEvaluationState.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_alert_notification_state_using_get**
> AlertNotificationState get_alert_notification_state_using_get(alert_id, project_id)

Get alert notification state by id

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.AlertingApi()
alert_id = 'alert_id_example' # str | alertId
project_id = 'project_id_example' # str | projectId

try:
    # Get alert notification state by id
    api_response = api_instance.get_alert_notification_state_using_get(alert_id, project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling AlertingApi->get_alert_notification_state_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **alert_id** | **str**| alertId | 
 **project_id** | **str**| projectId | 

### Return type

[**AlertNotificationState**](AlertNotificationState.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_alert_notification_stats_using_get**
> AlertNotificationState get_alert_notification_stats_using_get(alert_id, project_id)

Get alert notification stats by id

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.AlertingApi()
alert_id = 'alert_id_example' # str | alertId
project_id = 'project_id_example' # str | projectId

try:
    # Get alert notification stats by id
    api_response = api_instance.get_alert_notification_stats_using_get(alert_id, project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling AlertingApi->get_alert_notification_stats_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **alert_id** | **str**| alertId | 
 **project_id** | **str**| projectId | 

### Return type

[**AlertNotificationState**](AlertNotificationState.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_alert_using_get**
> Alert get_alert_using_get(alert_id, project_id)

Get alert by id

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.AlertingApi()
alert_id = 'alert_id_example' # str | alertId
project_id = 'project_id_example' # str | projectId

try:
    # Get alert by id
    api_response = api_instance.get_alert_using_get(alert_id, project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling AlertingApi->get_alert_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **alert_id** | **str**| alertId | 
 **project_id** | **str**| projectId | 

### Return type

[**Alert**](Alert.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_multi_alert_evaluation_state_using_get**
> AlertEvaluationState get_multi_alert_evaluation_state_using_get(alert_id, project_id)

Get alert evaluation stats by id

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.AlertingApi()
alert_id = 'alert_id_example' # str | alertId
project_id = 'project_id_example' # str | projectId

try:
    # Get alert evaluation stats by id
    api_response = api_instance.get_multi_alert_evaluation_state_using_get(alert_id, project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling AlertingApi->get_multi_alert_evaluation_state_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **alert_id** | **str**| alertId | 
 **project_id** | **str**| projectId | 

### Return type

[**AlertEvaluationState**](AlertEvaluationState.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_notification_using_get**
> NotificationChannel get_notification_using_get(notification_channel_id, project_id)

Get notification channel by id

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.AlertingApi()
notification_channel_id = 'notification_channel_id_example' # str | notificationChannelId
project_id = 'project_id_example' # str | projectId

try:
    # Get notification channel by id
    api_response = api_instance.get_notification_using_get(notification_channel_id, project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling AlertingApi->get_notification_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **notification_channel_id** | **str**| notificationChannelId | 
 **project_id** | **str**| projectId | 

### Return type

[**NotificationChannel**](NotificationChannel.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_project_stats_using_get**
> ProjectStatistics get_project_stats_using_get(project_id)

Get project stats

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.AlertingApi()
project_id = 'project_id_example' # str | projectId

try:
    # Get project stats
    api_response = api_instance.get_project_stats_using_get(project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling AlertingApi->get_project_stats_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **project_id** | **str**| projectId | 

### Return type

[**ProjectStatistics**](ProjectStatistics.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_sub_alert_evaluation_state_using_get**
> AlertEvaluationState get_sub_alert_evaluation_state_using_get(alert_id, parent_id, project_id)

Get sub alert evaluation state by id

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.AlertingApi()
alert_id = 'alert_id_example' # str | alertId
parent_id = 'parent_id_example' # str | parentId
project_id = 'project_id_example' # str | projectId

try:
    # Get sub alert evaluation state by id
    api_response = api_instance.get_sub_alert_evaluation_state_using_get(alert_id, parent_id, project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling AlertingApi->get_sub_alert_evaluation_state_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **alert_id** | **str**| alertId | 
 **parent_id** | **str**| parentId | 
 **project_id** | **str**| projectId | 

### Return type

[**AlertEvaluationState**](AlertEvaluationState.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_sub_alert_notification_state_using_get**
> AlertNotificationState get_sub_alert_notification_state_using_get(alert_id, parent_id, project_id)

Get sub alert notification state by id

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.AlertingApi()
alert_id = 'alert_id_example' # str | alertId
parent_id = 'parent_id_example' # str | parentId
project_id = 'project_id_example' # str | projectId

try:
    # Get sub alert notification state by id
    api_response = api_instance.get_sub_alert_notification_state_using_get(alert_id, parent_id, project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling AlertingApi->get_sub_alert_notification_state_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **alert_id** | **str**| alertId | 
 **parent_id** | **str**| parentId | 
 **project_id** | **str**| projectId | 

### Return type

[**AlertNotificationState**](AlertNotificationState.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_sub_alert_using_get**
> Alert get_sub_alert_using_get(alert_id, parent_id, project_id)

Get sub alert by id

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.AlertingApi()
alert_id = 'alert_id_example' # str | alertId
parent_id = 'parent_id_example' # str | parentId
project_id = 'project_id_example' # str | projectId

try:
    # Get sub alert by id
    api_response = api_instance.get_sub_alert_using_get(alert_id, parent_id, project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling AlertingApi->get_sub_alert_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **alert_id** | **str**| alertId | 
 **parent_id** | **str**| parentId | 
 **project_id** | **str**| projectId | 

### Return type

[**Alert**](Alert.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_telegram_group_titles_using_get**
> TelegramGroupTitlesResponseDto get_telegram_group_titles_using_get()

Get telegram group titles

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.AlertingApi()

try:
    # Get telegram group titles
    api_response = api_instance.get_telegram_group_titles_using_get()
    pprint(api_response)
except ApiException as e:
    print("Exception when calling AlertingApi->get_telegram_group_titles_using_get: %s\n" % e)
```

### Parameters
This endpoint does not need any parameter.

### Return type

[**TelegramGroupTitlesResponseDto**](TelegramGroupTitlesResponseDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_ya_chats_groups_using_get**
> YaChatsGroupsResponseDto get_ya_chats_groups_using_get()

Get Yandex Chats group titles and description

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.AlertingApi()

try:
    # Get Yandex Chats group titles and description
    api_response = api_instance.get_ya_chats_groups_using_get()
    pprint(api_response)
except ApiException as e:
    print("Exception when calling AlertingApi->get_ya_chats_groups_using_get: %s\n" % e)
```

### Parameters
This endpoint does not need any parameter.

### Return type

[**YaChatsGroupsResponseDto**](YaChatsGroupsResponseDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **list_alerts_by_parent_using_get**
> SubAlertPage list_alerts_by_parent_using_get(parent_id, project_id, annotation_keys=annotation_keys, filter_by_evaluation_status=filter_by_evaluation_status, filter_by_labels=filter_by_labels, filter_by_notification_ids=filter_by_notification_ids, filter_by_notification_status=filter_by_notification_status, order_by_labels=order_by_labels, page_size=page_size, page_token=page_token)

List sub alerts

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.AlertingApi()
parent_id = 'parent_id_example' # str | parentId
project_id = 'project_id_example' # str | projectId
annotation_keys = ['annotation_keys_example'] # list[str] | annotationKeys (optional)
filter_by_evaluation_status = ['filter_by_evaluation_status_example'] # list[str] | filterByEvaluationStatus (optional)
filter_by_labels = 'filter_by_labels_example' # str | filterByLabels (optional)
filter_by_notification_ids = ['filter_by_notification_ids_example'] # list[str] | filterByNotificationIds (optional)
filter_by_notification_status = ['filter_by_notification_status_example'] # list[str] | filterByNotificationStatus (optional)
order_by_labels = 'order_by_labels_example' # str | orderByLabels (optional)
page_size = 10 # int | pageSize (optional) (default to 10)
page_token = 'page_token_example' # str | pageToken (optional)

try:
    # List sub alerts
    api_response = api_instance.list_alerts_by_parent_using_get(parent_id, project_id, annotation_keys=annotation_keys, filter_by_evaluation_status=filter_by_evaluation_status, filter_by_labels=filter_by_labels, filter_by_notification_ids=filter_by_notification_ids, filter_by_notification_status=filter_by_notification_status, order_by_labels=order_by_labels, page_size=page_size, page_token=page_token)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling AlertingApi->list_alerts_by_parent_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **parent_id** | **str**| parentId | 
 **project_id** | **str**| projectId | 
 **annotation_keys** | [**list[str]**](str.md)| annotationKeys | [optional] 
 **filter_by_evaluation_status** | [**list[str]**](str.md)| filterByEvaluationStatus | [optional] 
 **filter_by_labels** | **str**| filterByLabels | [optional] 
 **filter_by_notification_ids** | [**list[str]**](str.md)| filterByNotificationIds | [optional] 
 **filter_by_notification_status** | [**list[str]**](str.md)| filterByNotificationStatus | [optional] 
 **order_by_labels** | **str**| orderByLabels | [optional] 
 **page_size** | **int**| pageSize | [optional] [default to 10]
 **page_token** | **str**| pageToken | [optional] 

### Return type

[**SubAlertPage**](SubAlertPage.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **list_alerts_by_project_using_get**
> AlertPage list_alerts_by_project_using_get(project_id, filter_by_evaluation_status=filter_by_evaluation_status, filter_by_name=filter_by_name, filter_by_notification_id=filter_by_notification_id, filter_by_notification_status=filter_by_notification_status, filter_by_states=filter_by_states, filter_by_types=filter_by_types, order_by_name=order_by_name, page_size=page_size, page_token=page_token)

List alerts

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.AlertingApi()
project_id = 'project_id_example' # str | projectId
filter_by_evaluation_status = ['filter_by_evaluation_status_example'] # list[str] | filterByEvaluationStatus (optional)
filter_by_name = 'filter_by_name_example' # str | filterByName (optional)
filter_by_notification_id = ['filter_by_notification_id_example'] # list[str] | filterByNotificationId (optional)
filter_by_notification_status = ['filter_by_notification_status_example'] # list[str] | filterByNotificationStatus (optional)
filter_by_states = ['filter_by_states_example'] # list[str] | filterByStates (optional)
filter_by_types = ['filter_by_types_example'] # list[str] | filterByTypes (optional)
order_by_name = 'order_by_name_example' # str | orderByName (optional)
page_size = 10 # int | pageSize (optional) (default to 10)
page_token = 'page_token_example' # str | pageToken (optional)

try:
    # List alerts
    api_response = api_instance.list_alerts_by_project_using_get(project_id, filter_by_evaluation_status=filter_by_evaluation_status, filter_by_name=filter_by_name, filter_by_notification_id=filter_by_notification_id, filter_by_notification_status=filter_by_notification_status, filter_by_states=filter_by_states, filter_by_types=filter_by_types, order_by_name=order_by_name, page_size=page_size, page_token=page_token)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling AlertingApi->list_alerts_by_project_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **project_id** | **str**| projectId | 
 **filter_by_evaluation_status** | [**list[str]**](str.md)| filterByEvaluationStatus | [optional] 
 **filter_by_name** | **str**| filterByName | [optional] 
 **filter_by_notification_id** | [**list[str]**](str.md)| filterByNotificationId | [optional] 
 **filter_by_notification_status** | [**list[str]**](str.md)| filterByNotificationStatus | [optional] 
 **filter_by_states** | [**list[str]**](str.md)| filterByStates | [optional] 
 **filter_by_types** | [**list[str]**](str.md)| filterByTypes | [optional] 
 **order_by_name** | **str**| orderByName | [optional] 
 **page_size** | **int**| pageSize | [optional] [default to 10]
 **page_token** | **str**| pageToken | [optional] 

### Return type

[**AlertPage**](AlertPage.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **list_notification_using_get**
> NotificationChannelPage list_notification_using_get(project_id, filter_by_name=filter_by_name, filter_by_type=filter_by_type, order_by_name=order_by_name, order_by_type=order_by_type, page_size=page_size, page_token=page_token)

List notification channels

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.AlertingApi()
project_id = 'project_id_example' # str | projectId
filter_by_name = 'filter_by_name_example' # str | filterByName (optional)
filter_by_type = ['filter_by_type_example'] # list[str] | filterByType (optional)
order_by_name = 'order_by_name_example' # str | orderByName (optional)
order_by_type = 'order_by_type_example' # str | orderByType (optional)
page_size = 10 # int | pageSize (optional) (default to 10)
page_token = 'page_token_example' # str | pageToken (optional)

try:
    # List notification channels
    api_response = api_instance.list_notification_using_get(project_id, filter_by_name=filter_by_name, filter_by_type=filter_by_type, order_by_name=order_by_name, order_by_type=order_by_type, page_size=page_size, page_token=page_token)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling AlertingApi->list_notification_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **project_id** | **str**| projectId | 
 **filter_by_name** | **str**| filterByName | [optional] 
 **filter_by_type** | [**list[str]**](str.md)| filterByType | [optional] 
 **order_by_name** | **str**| orderByName | [optional] 
 **order_by_type** | **str**| orderByType | [optional] 
 **page_size** | **int**| pageSize | [optional] [default to 10]
 **page_token** | **str**| pageToken | [optional] 

### Return type

[**NotificationChannelPage**](NotificationChannelPage.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **update_alert_using_put**
> Alert update_alert_using_put(body, alert_id, project_id)

Update alert by id

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.AlertingApi()
body = solomon_client.Alert() # Alert | alert
alert_id = 'alert_id_example' # str | alertId
project_id = 'project_id_example' # str | projectId

try:
    # Update alert by id
    api_response = api_instance.update_alert_using_put(body, alert_id, project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling AlertingApi->update_alert_using_put: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**Alert**](Alert.md)| alert | 
 **alert_id** | **str**| alertId | 
 **project_id** | **str**| projectId | 

### Return type

[**Alert**](Alert.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **update_notification_using_put**
> NotificationChannel update_notification_using_put(body, notification_channel_id, project_id)

Update notification channel by id

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.AlertingApi()
body = solomon_client.NotificationChannel() # NotificationChannel | notification
notification_channel_id = 'notification_channel_id_example' # str | notificationChannelId
project_id = 'project_id_example' # str | projectId

try:
    # Update notification channel by id
    api_response = api_instance.update_notification_using_put(body, notification_channel_id, project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling AlertingApi->update_notification_using_put: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**NotificationChannel**](NotificationChannel.md)| notification | 
 **notification_channel_id** | **str**| notificationChannelId | 
 **project_id** | **str**| projectId | 

### Return type

[**NotificationChannel**](NotificationChannel.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

