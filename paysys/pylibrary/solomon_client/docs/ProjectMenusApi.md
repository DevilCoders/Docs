# solomon_client.ProjectMenusApi

All URIs are relative to *//solomon.yandex-team.ru/*

Method | HTTP request | Description
------------- | ------------- | -------------
[**get_project_menu_using_get**](ProjectMenusApi.md#get_project_menu_using_get) | **GET** /api/v2/projects/{projectId}/menu | return project menu
[**save_project_menu_using_post**](ProjectMenusApi.md#save_project_menu_using_post) | **POST** /api/v2/projects/{projectId}/menu | save project menu
[**save_project_menu_using_put**](ProjectMenusApi.md#save_project_menu_using_put) | **PUT** /api/v2/projects/{projectId}/menu | save project menu

# **get_project_menu_using_get**
> ProjectMenuDto get_project_menu_using_get(project_id)

return project menu

This action returns Solomon frontend menu configuration for project.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.ProjectMenusApi()
project_id = 'project_id_example' # str | projectId

try:
    # return project menu
    api_response = api_instance.get_project_menu_using_get(project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling ProjectMenusApi->get_project_menu_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **project_id** | **str**| projectId | 

### Return type

[**ProjectMenuDto**](ProjectMenuDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **save_project_menu_using_post**
> ProjectMenuDto save_project_menu_using_post(body, project_id)

save project menu

This action will create or update already existed Solomon frontend menu configuration for project.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.ProjectMenusApi()
body = solomon_client.ProjectMenuDto() # ProjectMenuDto | projectMenu
project_id = 'project_id_example' # str | projectId

try:
    # save project menu
    api_response = api_instance.save_project_menu_using_post(body, project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling ProjectMenusApi->save_project_menu_using_post: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**ProjectMenuDto**](ProjectMenuDto.md)| projectMenu | 
 **project_id** | **str**| projectId | 

### Return type

[**ProjectMenuDto**](ProjectMenuDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **save_project_menu_using_put**
> ProjectMenuDto save_project_menu_using_put(body, project_id)

save project menu

This action will create or update already existed Solomon frontend menu configuration for project.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.ProjectMenusApi()
body = solomon_client.ProjectMenuDto() # ProjectMenuDto | projectMenu
project_id = 'project_id_example' # str | projectId

try:
    # save project menu
    api_response = api_instance.save_project_menu_using_put(body, project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling ProjectMenusApi->save_project_menu_using_put: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**ProjectMenuDto**](ProjectMenuDto.md)| projectMenu | 
 **project_id** | **str**| projectId | 

### Return type

[**ProjectMenuDto**](ProjectMenuDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

