# solomon_client.ClustersApi

All URIs are relative to *//solomon.yandex-team.ru/*

Method | HTTP request | Description
------------- | ------------- | -------------
[**create_cluster_using_post**](ClustersApi.md#create_cluster_using_post) | **POST** /api/v2/projects/{projectId}/clusters | create cluster
[**delete_cluster_using_delete**](ClustersApi.md#delete_cluster_using_delete) | **DELETE** /api/v2/projects/{projectId}/clusters/{clusterId} | delete cluster
[**get_all_using_get**](ClustersApi.md#get_all_using_get) | **GET** /api/v2/projects/{projectId}/clusters | list available clusters
[**get_cluster_services_using_get**](ClustersApi.md#get_cluster_services_using_get) | **GET** /api/v2/projects/{projectId}/clusters/{clusterId}/services | associated services
[**get_cluster_using_get**](ClustersApi.md#get_cluster_using_get) | **GET** /api/v2/projects/{projectId}/clusters/{clusterId} | read one cluster
[**update_cluster_using_put**](ClustersApi.md#update_cluster_using_put) | **PUT** /api/v2/projects/{projectId}/clusters/{clusterId} | update cluster

# **create_cluster_using_post**
> ClusterDto create_cluster_using_post(body, project_id)

create cluster

This action will save cluster document if there is no already existed cluster with given id.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.ClustersApi()
body = solomon_client.ClusterDto() # ClusterDto | cluster
project_id = 'project_id_example' # str | projectId

try:
    # create cluster
    api_response = api_instance.create_cluster_using_post(body, project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling ClustersApi->create_cluster_using_post: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**ClusterDto**](ClusterDto.md)| cluster | 
 **project_id** | **str**| projectId | 

### Return type

[**ClusterDto**](ClusterDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **delete_cluster_using_delete**
> delete_cluster_using_delete(cluster_id, project_id)

delete cluster

This action will delete already existed cluster.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.ClustersApi()
cluster_id = 'cluster_id_example' # str | clusterId
project_id = 'project_id_example' # str | projectId

try:
    # delete cluster
    api_instance.delete_cluster_using_delete(cluster_id, project_id)
except ApiException as e:
    print("Exception when calling ClustersApi->delete_cluster_using_delete: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **cluster_id** | **str**| clusterId | 
 **project_id** | **str**| projectId | 

### Return type

void (empty response body)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_all_using_get**
> PagedResultDtoClusterListItemDto get_all_using_get(project_id, page=page, page_size=page_size, text=text)

list available clusters

This action returns project's clusters if user have permissions to read that project.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.ClustersApi()
project_id = 'project_id_example' # str | projectId
page = solomon_client.Ref() # Ref | page number (starting from 0) (optional)
page_size = solomon_client.Ref() # Ref | page size (optional)
text = 'text_example' # str | text (optional)

try:
    # list available clusters
    api_response = api_instance.get_all_using_get(project_id, page=page, page_size=page_size, text=text)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling ClustersApi->get_all_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **project_id** | **str**| projectId | 
 **page** | [**Ref**](.md)| page number (starting from 0) | [optional] 
 **page_size** | [**Ref**](.md)| page size | [optional] 
 **text** | **str**| text | [optional] 

### Return type

[**PagedResultDtoClusterListItemDto**](PagedResultDtoClusterListItemDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_cluster_services_using_get**
> list[ClusterServiceAssociationDto] get_cluster_services_using_get(cluster_id, project_id)

associated services

This action returns services associated with cluster found by given clusterId.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.ClustersApi()
cluster_id = 'cluster_id_example' # str | clusterId
project_id = 'project_id_example' # str | projectId

try:
    # associated services
    api_response = api_instance.get_cluster_services_using_get(cluster_id, project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling ClustersApi->get_cluster_services_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **cluster_id** | **str**| clusterId | 
 **project_id** | **str**| projectId | 

### Return type

[**list[ClusterServiceAssociationDto]**](ClusterServiceAssociationDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_cluster_using_get**
> ClusterDto get_cluster_using_get(cluster_id, project_id)

read one cluster

This action returns single project's cluster found by given clusterId.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.ClustersApi()
cluster_id = 'cluster_id_example' # str | clusterId
project_id = 'project_id_example' # str | projectId

try:
    # read one cluster
    api_response = api_instance.get_cluster_using_get(cluster_id, project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling ClustersApi->get_cluster_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **cluster_id** | **str**| clusterId | 
 **project_id** | **str**| projectId | 

### Return type

[**ClusterDto**](ClusterDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **update_cluster_using_put**
> ClusterDto update_cluster_using_put(body, cluster_id, project_id)

update cluster

This action will update already existed project's cluster with given document.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.ClustersApi()
body = solomon_client.ClusterDto() # ClusterDto | cluster
cluster_id = 'cluster_id_example' # str | clusterId
project_id = 'project_id_example' # str | projectId

try:
    # update cluster
    api_response = api_instance.update_cluster_using_put(body, cluster_id, project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling ClustersApi->update_cluster_using_put: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**ClusterDto**](ClusterDto.md)| cluster | 
 **cluster_id** | **str**| clusterId | 
 **project_id** | **str**| projectId | 

### Return type

[**ClusterDto**](ClusterDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

