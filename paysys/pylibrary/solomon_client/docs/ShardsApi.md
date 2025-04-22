# solomon_client.ShardsApi

All URIs are relative to *//solomon.yandex-team.ru/*

Method | HTTP request | Description
------------- | ------------- | -------------
[**create_shard_using_post**](ShardsApi.md#create_shard_using_post) | **POST** /api/v2/projects/{projectId}/shards | create shard
[**delete_shard_using_delete**](ShardsApi.md#delete_shard_using_delete) | **DELETE** /api/v2/projects/{projectId}/shards/{shardId} | delete shard
[**get_all_using_get4**](ShardsApi.md#get_all_using_get4) | **GET** /api/v2/projects/{projectId}/shards | list available shards
[**get_shard_using_get**](ShardsApi.md#get_shard_using_get) | **GET** /api/v2/projects/{projectId}/shards/{shardId} | read one shard
[**targets_status_using_get**](ShardsApi.md#targets_status_using_get) | **GET** /api/v2/projects/{projectId}/shards/{shardId}/targets | get shard targets statuses
[**update_shard_using_put**](ShardsApi.md#update_shard_using_put) | **PUT** /api/v2/projects/{projectId}/shards/{shardId} | update shard

# **create_shard_using_post**
> ShardDto create_shard_using_post(body, project_id)

create shard

This action will save shard document if there is no already existed shard with given id.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.ShardsApi()
body = solomon_client.ShardDto() # ShardDto | shard
project_id = 'project_id_example' # str | projectId

try:
    # create shard
    api_response = api_instance.create_shard_using_post(body, project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling ShardsApi->create_shard_using_post: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**ShardDto**](ShardDto.md)| shard | 
 **project_id** | **str**| projectId | 

### Return type

[**ShardDto**](ShardDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **delete_shard_using_delete**
> delete_shard_using_delete(project_id, shard_id)

delete shard

This action will delete already existed shard.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.ShardsApi()
project_id = 'project_id_example' # str | projectId
shard_id = 'shard_id_example' # str | shardId

try:
    # delete shard
    api_instance.delete_shard_using_delete(project_id, shard_id)
except ApiException as e:
    print("Exception when calling ShardsApi->delete_shard_using_delete: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **project_id** | **str**| projectId | 
 **shard_id** | **str**| shardId | 

### Return type

void (empty response body)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_all_using_get4**
> PagedResultDtoShardListItemDto get_all_using_get4(project_id, page=page, page_size=page_size, state=state, text=text)

list available shards

This action returns project's shards if user have permissions to read that project.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.ShardsApi()
project_id = 'project_id_example' # str | projectId
page = solomon_client.Ref() # Ref | page number (starting from 0) (optional)
page_size = solomon_client.Ref() # Ref | page size (optional)
state = 'RW' # str | state (optional) (default to RW)
text = 'text_example' # str | text (optional)

try:
    # list available shards
    api_response = api_instance.get_all_using_get4(project_id, page=page, page_size=page_size, state=state, text=text)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling ShardsApi->get_all_using_get4: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **project_id** | **str**| projectId | 
 **page** | [**Ref**](.md)| page number (starting from 0) | [optional] 
 **page_size** | [**Ref**](.md)| page size | [optional] 
 **state** | **str**| state | [optional] [default to RW]
 **text** | **str**| text | [optional] 

### Return type

[**PagedResultDtoShardListItemDto**](PagedResultDtoShardListItemDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_shard_using_get**
> ShardDto get_shard_using_get(project_id, shard_id)

read one shard

This action returns single project's shard found by given shardId.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.ShardsApi()
project_id = 'project_id_example' # str | projectId
shard_id = 'shard_id_example' # str | shardId

try:
    # read one shard
    api_response = api_instance.get_shard_using_get(project_id, shard_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling ShardsApi->get_shard_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **project_id** | **str**| projectId | 
 **shard_id** | **str**| shardId | 

### Return type

[**ShardDto**](ShardDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **targets_status_using_get**
> ShardTargetStatusDtoPage targets_status_using_get(project_id, shard_id, dc=dc, fetcher_host=fetcher_host, host_glob=host_glob, status=status)

get shard targets statuses

This action will retrieve paged list of statuses of pulled shard targets by particular Solomon Fetcher host.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.ShardsApi()
project_id = 'project_id_example' # str | projectId
shard_id = 'shard_id_example' # str | shardId
dc = 'dc_example' # str | dc (optional)
fetcher_host = 'fetcher_host_example' # str | fetcherHost (optional)
host_glob = 'host_glob_example' # str | hostGlob (optional)
status = 'status_example' # str | status (optional)

try:
    # get shard targets statuses
    api_response = api_instance.targets_status_using_get(project_id, shard_id, dc=dc, fetcher_host=fetcher_host, host_glob=host_glob, status=status)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling ShardsApi->targets_status_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **project_id** | **str**| projectId | 
 **shard_id** | **str**| shardId | 
 **dc** | **str**| dc | [optional] 
 **fetcher_host** | **str**| fetcherHost | [optional] 
 **host_glob** | **str**| hostGlob | [optional] 
 **status** | **str**| status | [optional] 

### Return type

[**ShardTargetStatusDtoPage**](ShardTargetStatusDtoPage.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **update_shard_using_put**
> ShardDto update_shard_using_put(body, project_id, shard_id)

update shard

This action will update already existed project's shard with given document.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.ShardsApi()
body = solomon_client.ShardDto() # ShardDto | shard
project_id = 'project_id_example' # str | projectId
shard_id = 'shard_id_example' # str | shardId

try:
    # update shard
    api_response = api_instance.update_shard_using_put(body, project_id, shard_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling ShardsApi->update_shard_using_put: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**ShardDto**](ShardDto.md)| shard | 
 **project_id** | **str**| projectId | 
 **shard_id** | **str**| shardId | 

### Return type

[**ShardDto**](ShardDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

