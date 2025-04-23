# aioalexandria.ModelInfoApi

All URIs are relative to *http://localhost:9999/api/v1/*

Method | HTTP request | Description
------------- | ------------- | -------------
[**model_info_get**](ModelInfoApi.md#model_info_get) | **GET** /model_info/ | List model info.
[**model_info_id_delete**](ModelInfoApi.md#model_info_id_delete) | **DELETE** /model_info/{id} | Delete model info.
[**model_info_id_get**](ModelInfoApi.md#model_info_id_get) | **GET** /model_info/{id} | Get model info.
[**model_info_post**](ModelInfoApi.md#model_info_post) | **POST** /model_info/ | Create model info.

# **model_info_get**
> list[ModelInfo] model_info_get(ids=ids, soft_ids=soft_ids)

List model info.

show model info list

### Example
```python
from __future__ import print_function
import time
import aioalexandria
from aioalexandria.rest import ApiException
from pprint import pprint

# Configure API key authorization: Token
configuration = aioalexandria.Configuration()
configuration.api_key['Authorization'] = 'YOUR_API_KEY'
# Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
# configuration.api_key_prefix['Authorization'] = 'Bearer'

# create an instance of the API class
api_instance = aioalexandria.ModelInfoApi(aioalexandria.ApiClient(configuration))
ids = ['ids_example'] # list[str] | filter by ids (optional)
soft_ids = ['soft_ids_example'] # list[str] | filter by soft ids (optional)

try:
    # List model info.
    api_response = api_instance.model_info_get(ids=ids, soft_ids=soft_ids)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling ModelInfoApi->model_info_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **ids** | [**list[str]**](str.md)| filter by ids | [optional] 
 **soft_ids** | [**list[str]**](str.md)| filter by soft ids | [optional] 

### Return type

[**list[ModelInfo]**](ModelInfo.md)

### Authorization

[Token](../README.md#Token)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **model_info_id_delete**
> model_info_id_delete(id)

Delete model info.

remove model info

### Example
```python
from __future__ import print_function
import time
import aioalexandria
from aioalexandria.rest import ApiException
from pprint import pprint

# Configure API key authorization: Token
configuration = aioalexandria.Configuration()
configuration.api_key['Authorization'] = 'YOUR_API_KEY'
# Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
# configuration.api_key_prefix['Authorization'] = 'Bearer'

# create an instance of the API class
api_instance = aioalexandria.ModelInfoApi(aioalexandria.ApiClient(configuration))
id = 'id_example' # str | ID

try:
    # Delete model info.
    api_instance.model_info_id_delete(id)
except ApiException as e:
    print("Exception when calling ModelInfoApi->model_info_id_delete: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **id** | **str**| ID | 

### Return type

void (empty response body)

### Authorization

[Token](../README.md#Token)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **model_info_id_get**
> ModelInfo model_info_id_get(id)

Get model info.

show model info

### Example
```python
from __future__ import print_function
import time
import aioalexandria
from aioalexandria.rest import ApiException
from pprint import pprint

# Configure API key authorization: Token
configuration = aioalexandria.Configuration()
configuration.api_key['Authorization'] = 'YOUR_API_KEY'
# Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
# configuration.api_key_prefix['Authorization'] = 'Bearer'

# create an instance of the API class
api_instance = aioalexandria.ModelInfoApi(aioalexandria.ApiClient(configuration))
id = 'id_example' # str | ID

try:
    # Get model info.
    api_response = api_instance.model_info_id_get(id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling ModelInfoApi->model_info_id_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **id** | **str**| ID | 

### Return type

[**ModelInfo**](ModelInfo.md)

### Authorization

[Token](../README.md#Token)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **model_info_post**
> ModelInfo model_info_post(body)

Create model info.

create model info

### Example
```python
from __future__ import print_function
import time
import aioalexandria
from aioalexandria.rest import ApiException
from pprint import pprint

# Configure API key authorization: Token
configuration = aioalexandria.Configuration()
configuration.api_key['Authorization'] = 'YOUR_API_KEY'
# Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
# configuration.api_key_prefix['Authorization'] = 'Bearer'

# create an instance of the API class
api_instance = aioalexandria.ModelInfoApi(aioalexandria.ApiClient(configuration))
body = aioalexandria.ModelInfoPostRequest() # ModelInfoPostRequest | Post model info request

try:
    # Create model info.
    api_response = api_instance.model_info_post(body)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling ModelInfoApi->model_info_post: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**ModelInfoPostRequest**](ModelInfoPostRequest.md)| Post model info request | 

### Return type

[**ModelInfo**](ModelInfo.md)

### Authorization

[Token](../README.md#Token)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

