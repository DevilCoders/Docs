# solomon_client.GraphsApi

All URIs are relative to *//solomon.yandex-team.ru/*

Method | HTTP request | Description
------------- | ------------- | -------------
[**create_graph_using_post**](GraphsApi.md#create_graph_using_post) | **POST** /api/v2/projects/{projectId}/graphs | create graph
[**delete_graph_using_delete**](GraphsApi.md#delete_graph_using_delete) | **DELETE** /api/v2/projects/{projectId}/graphs/{graphId} | delete graph
[**get_all_using_get2**](GraphsApi.md#get_all_using_get2) | **GET** /api/v2/projects/{projectId}/graphs | list available graphs
[**get_graph_using_get**](GraphsApi.md#get_graph_using_get) | **GET** /api/v2/projects/{projectId}/graphs/{graphId} | read one graph
[**update_graph_using_put**](GraphsApi.md#update_graph_using_put) | **PUT** /api/v2/projects/{projectId}/graphs/{graphId} | update graph

# **create_graph_using_post**
> GraphDto create_graph_using_post(body, project_id)

create graph

This action will save graph document if there is no already existed graph with given id.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.GraphsApi()
body = solomon_client.GraphDto() # GraphDto | graph
project_id = 'project_id_example' # str | projectId

try:
    # create graph
    api_response = api_instance.create_graph_using_post(body, project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling GraphsApi->create_graph_using_post: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**GraphDto**](GraphDto.md)| graph | 
 **project_id** | **str**| projectId | 

### Return type

[**GraphDto**](GraphDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **delete_graph_using_delete**
> delete_graph_using_delete(graph_id, project_id)

delete graph

This action will delete already existed graph.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.GraphsApi()
graph_id = 'graph_id_example' # str | graphId
project_id = 'project_id_example' # str | projectId

try:
    # delete graph
    api_instance.delete_graph_using_delete(graph_id, project_id)
except ApiException as e:
    print("Exception when calling GraphsApi->delete_graph_using_delete: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **graph_id** | **str**| graphId | 
 **project_id** | **str**| projectId | 

### Return type

void (empty response body)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_all_using_get2**
> PagedResultDtoGraphListItemDto get_all_using_get2(project_id, page=page, page_size=page_size, text=text)

list available graphs

This action returns project's graphs if user have permissions to read that project.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.GraphsApi()
project_id = 'project_id_example' # str | projectId
page = solomon_client.Ref() # Ref | page number (starting from 0) (optional)
page_size = solomon_client.Ref() # Ref | page size (optional)
text = 'text_example' # str | text filter by id (optional)

try:
    # list available graphs
    api_response = api_instance.get_all_using_get2(project_id, page=page, page_size=page_size, text=text)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling GraphsApi->get_all_using_get2: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **project_id** | **str**| projectId | 
 **page** | [**Ref**](.md)| page number (starting from 0) | [optional] 
 **page_size** | [**Ref**](.md)| page size | [optional] 
 **text** | **str**| text filter by id | [optional] 

### Return type

[**PagedResultDtoGraphListItemDto**](PagedResultDtoGraphListItemDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_graph_using_get**
> GraphDto get_graph_using_get(graph_id, project_id)

read one graph

This action returns single project's graph found by given graphId.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.GraphsApi()
graph_id = 'graph_id_example' # str | graphId
project_id = 'project_id_example' # str | projectId

try:
    # read one graph
    api_response = api_instance.get_graph_using_get(graph_id, project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling GraphsApi->get_graph_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **graph_id** | **str**| graphId | 
 **project_id** | **str**| projectId | 

### Return type

[**GraphDto**](GraphDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **update_graph_using_put**
> GraphDto update_graph_using_put(body, graph_id, project_id)

update graph

This action will update already existed project's graph with given document.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.GraphsApi()
body = solomon_client.GraphDto() # GraphDto | graph
graph_id = 'graph_id_example' # str | graphId
project_id = 'project_id_example' # str | projectId

try:
    # update graph
    api_response = api_instance.update_graph_using_put(body, graph_id, project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling GraphsApi->update_graph_using_put: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**GraphDto**](GraphDto.md)| graph | 
 **graph_id** | **str**| graphId | 
 **project_id** | **str**| projectId | 

### Return type

[**GraphDto**](GraphDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

