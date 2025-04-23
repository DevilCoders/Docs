# solomon_client.DataApi

All URIs are relative to *//solomon.yandex-team.ru/*

Method | HTTP request | Description
------------- | ------------- | -------------
[**read_data_from_json_using_post**](DataApi.md#read_data_from_json_using_post) | **POST** /api/v2/projects/{projectId}/sensors/data | compute sensors data

# **read_data_from_json_using_post**
> DataResult read_data_from_json_using_post(body, project_id)

compute sensors data

This action returns data by Solomon-specific program if user have permissions to read that project.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.DataApi()
body = solomon_client.DataRequest() # DataRequest | requestDto
project_id = 'project_id_example' # str | projectId

try:
    # compute sensors data
    api_response = api_instance.read_data_from_json_using_post(body, project_id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling DataApi->read_data_from_json_using_post: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**DataRequest**](DataRequest.md)| requestDto | 
 **project_id** | **str**| projectId | 

### Return type

[**DataResult**](DataResult.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json;charset=UTF-8
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

