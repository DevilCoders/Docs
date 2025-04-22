# solomon_client.ServicesApi

All URIs are relative to *//solomon.yandex-team.ru/*

Method | HTTP request | Description
------------- | ------------- | -------------
[**create_service_using_post**](ServicesApi.md#create_service_using_post) | **POST** /api/v2/projects/{projectId}/services | create service
[**delete_service_using_delete**](ServicesApi.md#delete_service_using_delete) | **DELETE** /api/v2/projects/{projectId}/services/{serviceId} | delete service
[**get_all_using_get3**](ServicesApi.md#get_all_using_get3) | **GET** /api/v2/projects/{projectId}/services | list available services
[**get_service_clusters_using_get**](ServicesApi.md#get_service_clusters_using_get) | **GET** /api/v2/projects/{projectId}/services/{serviceId}/clusters | associated clusters
[**get_service_using_get**](ServicesApi.md#get_service_using_get) | **GET** /api/v2/projects/{projectId}/services/{serviceId} | read one service
[**update_service_using_put**](ServicesApi.md#update_service_using_put) | **PUT** /api/v2/projects/{projectId}/services/{serviceId} | update service

# **create_service_using_post**
> ServiceDto create_service_using_post(body, project_id)

create service

This action will save service document if there is no already existed service with given id.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.ServicesApi()
body = solomon_client.ServiceDto() # ServiceDto | service
project_id = 'project_id_example' # str | projectId

try:
    # create service
    api_response = api_instance.create_service_using_post(body, project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling ServicesApi->create_service_using_post: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**ServiceDto**](ServiceDto.md)| service | 
 **project_id** | **str**| projectId | 

### Return type

[**ServiceDto**](ServiceDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **delete_service_using_delete**
> delete_service_using_delete(project_id, service_id)

delete service

This action will delete already existed service.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.ServicesApi()
project_id = 'project_id_example' # str | projectId
service_id = 'service_id_example' # str | serviceId

try:
    # delete service
    api_instance.delete_service_using_delete(project_id, service_id)
except ApiException as e:
    print("Exception when calling ServicesApi->delete_service_using_delete: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **project_id** | **str**| projectId | 
 **service_id** | **str**| serviceId | 

### Return type

void (empty response body)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_all_using_get3**
> PagedResultDtoServiceListItemDto get_all_using_get3(project_id, page=page, page_size=page_size, text=text)

list available services

This action returns project's services if user have permissions to read that project.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.ServicesApi()
project_id = 'project_id_example' # str | projectId
page = solomon_client.Ref() # Ref | page number (starting from 0) (optional)
page_size = solomon_client.Ref() # Ref | page size (optional)
text = 'text_example' # str | text (optional)

try:
    # list available services
    api_response = api_instance.get_all_using_get3(project_id, page=page, page_size=page_size, text=text)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling ServicesApi->get_all_using_get3: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **project_id** | **str**| projectId | 
 **page** | [**Ref**](.md)| page number (starting from 0) | [optional] 
 **page_size** | [**Ref**](.md)| page size | [optional] 
 **text** | **str**| text | [optional] 

### Return type

[**PagedResultDtoServiceListItemDto**](PagedResultDtoServiceListItemDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_service_clusters_using_get**
> list[ClusterServiceAssociationDto] get_service_clusters_using_get(project_id, service_id)

associated clusters

This action returns clusters associated with service found by given serviceId.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.ServicesApi()
project_id = 'project_id_example' # str | projectId
service_id = 'service_id_example' # str | serviceId

try:
    # associated clusters
    api_response = api_instance.get_service_clusters_using_get(project_id, service_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling ServicesApi->get_service_clusters_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **project_id** | **str**| projectId | 
 **service_id** | **str**| serviceId | 

### Return type

[**list[ClusterServiceAssociationDto]**](ClusterServiceAssociationDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_service_using_get**
> ServiceDto get_service_using_get(project_id, service_id)

read one service

This action returns single project's service found by given serviceId.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.ServicesApi()
project_id = 'project_id_example' # str | projectId
service_id = 'service_id_example' # str | serviceId

try:
    # read one service
    api_response = api_instance.get_service_using_get(project_id, service_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling ServicesApi->get_service_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **project_id** | **str**| projectId | 
 **service_id** | **str**| serviceId | 

### Return type

[**ServiceDto**](ServiceDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **update_service_using_put**
> ServiceDto update_service_using_put(body, project_id, service_id)

update service

This action will update already existed project's service with given document.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.ServicesApi()
body = solomon_client.ServiceDto() # ServiceDto | service
project_id = 'project_id_example' # str | projectId
service_id = 'service_id_example' # str | serviceId

try:
    # update service
    api_response = api_instance.update_service_using_put(body, project_id, service_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling ServicesApi->update_service_using_put: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**ServiceDto**](ServiceDto.md)| service | 
 **project_id** | **str**| projectId | 
 **service_id** | **str**| serviceId | 

### Return type

[**ServiceDto**](ServiceDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

