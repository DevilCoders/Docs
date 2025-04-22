# solomon_client.ProjectsApi

All URIs are relative to *//solomon.yandex-team.ru/*

Method | HTTP request | Description
------------- | ------------- | -------------
[**all_projects_using_get**](ProjectsApi.md#all_projects_using_get) | **GET** /api/v2/projects | list available projects
[**create_project_using_post**](ProjectsApi.md#create_project_using_post) | **POST** /api/v2/projects | create project
[**delete_project_using_delete1**](ProjectsApi.md#delete_project_using_delete1) | **DELETE** /api/v2/projects/{id} | delete project
[**get_project_using_get**](ProjectsApi.md#get_project_using_get) | **GET** /api/v2/projects/{id} | read one project
[**update_project_using_put**](ProjectsApi.md#update_project_using_put) | **PUT** /api/v2/projects/{id} | update project

# **all_projects_using_get**
> object all_projects_using_get(use_pagination=use_pagination, filter_by_permissions=filter_by_permissions, page=page, page_size=page_size, text=text)

list available projects

This action returns all available for current user projects.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.ProjectsApi()
use_pagination = false # bool | _usePagination (optional) (default to false)
filter_by_permissions = solomon_client.Ref() # Ref | filter projects by project permissions for current user (optional)
page = solomon_client.Ref() # Ref | page number (starting from 0) (optional)
page_size = solomon_client.Ref() # Ref | page size (optional)
text = 'text_example' # str | filter projects by id or name (optional)

try:
    # list available projects
    api_response = api_instance.all_projects_using_get(use_pagination=use_pagination, filter_by_permissions=filter_by_permissions, page=page, page_size=page_size, text=text)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling ProjectsApi->all_projects_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **use_pagination** | **bool**| _usePagination | [optional] [default to false]
 **filter_by_permissions** | [**Ref**](.md)| filter projects by project permissions for current user | [optional] 
 **page** | [**Ref**](.md)| page number (starting from 0) | [optional] 
 **page_size** | [**Ref**](.md)| page size | [optional] 
 **text** | **str**| filter projects by id or name | [optional] 

### Return type

**object**

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **create_project_using_post**
> ProjectDto create_project_using_post(body, authorization)

create project

This action will save project document if there is no already existed project with given id.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.ProjectsApi()
body = solomon_client.ProjectDto() # ProjectDto | project
authorization = 'authorization_example' # str | Authorization

try:
    # create project
    api_response = api_instance.create_project_using_post(body, authorization)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling ProjectsApi->create_project_using_post: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**ProjectDto**](ProjectDto.md)| project | 
 **authorization** | **str**| Authorization | 

### Return type

[**ProjectDto**](ProjectDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **delete_project_using_delete1**
> delete_project_using_delete1(id)

delete project

This action will delete already existed project.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.ProjectsApi()
id = 'id_example' # str | id

try:
    # delete project
    api_instance.delete_project_using_delete1(id)
except ApiException as e:
    print("Exception when calling ProjectsApi->delete_project_using_delete1: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **id** | **str**| id | 

### Return type

void (empty response body)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_project_using_get**
> ProjectDto get_project_using_get(id)

read one project

This action returns single project found by given id.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.ProjectsApi()
id = 'id_example' # str | id

try:
    # read one project
    api_response = api_instance.get_project_using_get(id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling ProjectsApi->get_project_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **id** | **str**| id | 

### Return type

[**ProjectDto**](ProjectDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **update_project_using_put**
> ProjectDto update_project_using_put(body, authorization, id)

update project

This action will update already existed project with given document.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.ProjectsApi()
body = solomon_client.ProjectDto() # ProjectDto | project
authorization = 'authorization_example' # str | Authorization
id = 'id_example' # str | id

try:
    # update project
    api_response = api_instance.update_project_using_put(body, authorization, id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling ProjectsApi->update_project_using_put: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**ProjectDto**](ProjectDto.md)| project | 
 **authorization** | **str**| Authorization | 
 **id** | **str**| id | 

### Return type

[**ProjectDto**](ProjectDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

