# solomon_client.PushApi

All URIs are relative to *//solomon.yandex-team.ru/*

Method | HTTP request | Description
------------- | ------------- | -------------
[**push_using_post**](PushApi.md#push_using_post) | **POST** /api/v2/push | Push sensors data

# **push_using_post**
> PushResultDto push_using_post(cluster, project, service, body=body, auth_type=auth_type, request_id=request_id, unique_id=unique_id)

Push sensors data

This action pushes data to Solomon (recommended). See https://wiki.yandex-team.ru/solomon/api/push/ for more information.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.PushApi()
cluster = 'cluster_example' # str | Cluster label name to push data
project = 'project_example' # str | Project to push data
service = 'service_example' # str | Service label name to push data
body = 'body_example' # str | Sensors data in JSON or SPACK format. Format determined by Content-Type header (optional)
auth_type = 'auth_type_example' # str |  (optional)
request_id = 'request_id_example' # str | requestId (optional)
unique_id = 'unique_id_example' # str |  (optional)

try:
    # Push sensors data
    api_response = api_instance.push_using_post(cluster, project, service, body=body, auth_type=auth_type, request_id=request_id, unique_id=unique_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling PushApi->push_using_post: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **cluster** | **str**| Cluster label name to push data | 
 **project** | **str**| Project to push data | 
 **service** | **str**| Service label name to push data | 
 **body** | [**str**](str.md)| Sensors data in JSON or SPACK format. Format determined by Content-Type header | [optional] 
 **auth_type** | **str**|  | [optional] 
 **request_id** | **str**| requestId | [optional] 
 **unique_id** | **str**|  | [optional] 

### Return type

[**PushResultDto**](PushResultDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

