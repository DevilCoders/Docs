# solomon_client.YasmAlertingApi

All URIs are relative to *//solomon.yandex-team.ru/*

Method | HTTP request | Description
------------- | ------------- | -------------
[**convert_using_post**](YasmAlertingApi.md#convert_using_post) | **POST** /api/v2/yasmAlerts/convert | Validate and convert Yasm alerts

# **convert_using_post**
> ConvertAlertsResponseDto convert_using_post(body)

Validate and convert Yasm alerts

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.YasmAlertingApi()
body = solomon_client.ConvertAlertsRequest() # ConvertAlertsRequest | request

try:
    # Validate and convert Yasm alerts
    api_response = api_instance.convert_using_post(body)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling YasmAlertingApi->convert_using_post: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**ConvertAlertsRequest**](ConvertAlertsRequest.md)| request | 

### Return type

[**ConvertAlertsResponseDto**](ConvertAlertsResponseDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

