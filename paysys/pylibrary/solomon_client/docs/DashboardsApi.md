# solomon_client.DashboardsApi

All URIs are relative to *//solomon.yandex-team.ru/*

Method | HTTP request | Description
------------- | ------------- | -------------
[**create_dashboard_using_post**](DashboardsApi.md#create_dashboard_using_post) | **POST** /api/v2/projects/{projectId}/dashboards | create dashboard
[**delete_project_using_delete**](DashboardsApi.md#delete_project_using_delete) | **DELETE** /api/v2/projects/{projectId}/dashboards/{dashboardId} | delete dashboard
[**get_all_using_get1**](DashboardsApi.md#get_all_using_get1) | **GET** /api/v2/projects/{projectId}/dashboards | list available dashboards
[**get_dashboard_using_get**](DashboardsApi.md#get_dashboard_using_get) | **GET** /api/v2/projects/{projectId}/dashboards/{dashboardId} | read one dashboard
[**update_dashboard_using_put**](DashboardsApi.md#update_dashboard_using_put) | **PUT** /api/v2/projects/{projectId}/dashboards/{dashboardId} | update dashboard

# **create_dashboard_using_post**
> DashboardDto create_dashboard_using_post(body, project_id)

create dashboard

This action will save dashboard document if there is no already existed dashboard with given id.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.DashboardsApi()
body = solomon_client.DashboardDto() # DashboardDto | dashboard
project_id = 'project_id_example' # str | projectId

try:
    # create dashboard
    api_response = api_instance.create_dashboard_using_post(body, project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling DashboardsApi->create_dashboard_using_post: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**DashboardDto**](DashboardDto.md)| dashboard | 
 **project_id** | **str**| projectId | 

### Return type

[**DashboardDto**](DashboardDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **delete_project_using_delete**
> delete_project_using_delete(dashboard_id, project_id)

delete dashboard

This action will delete already existed dashboard.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.DashboardsApi()
dashboard_id = 'dashboard_id_example' # str | dashboardId
project_id = 'project_id_example' # str | projectId

try:
    # delete dashboard
    api_instance.delete_project_using_delete(dashboard_id, project_id)
except ApiException as e:
    print("Exception when calling DashboardsApi->delete_project_using_delete: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **dashboard_id** | **str**| dashboardId | 
 **project_id** | **str**| projectId | 

### Return type

void (empty response body)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_all_using_get1**
> PagedResultDtoDashboardListItemDto get_all_using_get1(project_id, page=page, page_size=page_size, text=text)

list available dashboards

This action returns project's dashboards if user have permissions to read that project.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.DashboardsApi()
project_id = 'project_id_example' # str | projectId
page = solomon_client.Ref() # Ref | page number (starting from 0) (optional)
page_size = solomon_client.Ref() # Ref | page size (optional)
text = 'text_example' # str | text filter by id (optional)

try:
    # list available dashboards
    api_response = api_instance.get_all_using_get1(project_id, page=page, page_size=page_size, text=text)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling DashboardsApi->get_all_using_get1: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **project_id** | **str**| projectId | 
 **page** | [**Ref**](.md)| page number (starting from 0) | [optional] 
 **page_size** | [**Ref**](.md)| page size | [optional] 
 **text** | **str**| text filter by id | [optional] 

### Return type

[**PagedResultDtoDashboardListItemDto**](PagedResultDtoDashboardListItemDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_dashboard_using_get**
> DashboardDto get_dashboard_using_get(dashboard_id, project_id)

read one dashboard

This action returns single project's dashboard found by given dashboardId.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.DashboardsApi()
dashboard_id = 'dashboard_id_example' # str | dashboardId
project_id = 'project_id_example' # str | projectId

try:
    # read one dashboard
    api_response = api_instance.get_dashboard_using_get(dashboard_id, project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling DashboardsApi->get_dashboard_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **dashboard_id** | **str**| dashboardId | 
 **project_id** | **str**| projectId | 

### Return type

[**DashboardDto**](DashboardDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **update_dashboard_using_put**
> DashboardDto update_dashboard_using_put(body, dashboard_id, project_id)

update dashboard

This action will update already existed project's dashboard with given document.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.DashboardsApi()
body = solomon_client.DashboardDto() # DashboardDto | dashboard
dashboard_id = 'dashboard_id_example' # str | dashboardId
project_id = 'project_id_example' # str | projectId

try:
    # update dashboard
    api_response = api_instance.update_dashboard_using_put(body, dashboard_id, project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling DashboardsApi->update_dashboard_using_put: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**DashboardDto**](DashboardDto.md)| dashboard | 
 **dashboard_id** | **str**| dashboardId | 
 **project_id** | **str**| projectId | 

### Return type

[**DashboardDto**](DashboardDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

