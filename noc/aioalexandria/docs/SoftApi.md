# aioalexandria.SoftApi

All URIs are relative to *http://localhost:9999/api/v1/*

Method | HTTP request | Description
------------- | ------------- | -------------
[**soft_get**](SoftApi.md#soft_get) | **GET** /soft/ | List soft.
[**soft_id_delete**](SoftApi.md#soft_id_delete) | **DELETE** /soft/{id} | Delete soft.
[**soft_id_get**](SoftApi.md#soft_id_get) | **GET** /soft/{id} | Get soft.
[**soft_post**](SoftApi.md#soft_post) | **POST** /soft/ | Create soft.

# **soft_get**
> list[Soft] soft_get(version=version, ids=ids)

List soft.

show soft list

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
api_instance = aioalexandria.SoftApi(aioalexandria.ApiClient(configuration))
version = 'version_example' # str | filter by version (optional)
ids = ['ids_example'] # list[str] | filter by ids (optional)

try:
    # List soft.
    api_response = api_instance.soft_get(version=version, ids=ids)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling SoftApi->soft_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **version** | **str**| filter by version | [optional] 
 **ids** | [**list[str]**](str.md)| filter by ids | [optional] 

### Return type

[**list[Soft]**](Soft.md)

### Authorization

[Token](../README.md#Token)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **soft_id_delete**
> soft_id_delete(id)

Delete soft.

remove soft

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
api_instance = aioalexandria.SoftApi(aioalexandria.ApiClient(configuration))
id = 'id_example' # str | ID

try:
    # Delete soft.
    api_instance.soft_id_delete(id)
except ApiException as e:
    print("Exception when calling SoftApi->soft_id_delete: %s\n" % e)
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

# **soft_id_get**
> Soft soft_id_get(id)

Get soft.

show soft

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
api_instance = aioalexandria.SoftApi(aioalexandria.ApiClient(configuration))
id = 'id_example' # str | ID

try:
    # Get soft.
    api_response = api_instance.soft_id_get(id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling SoftApi->soft_id_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **id** | **str**| ID | 

### Return type

[**Soft**](Soft.md)

### Authorization

[Token](../README.md#Token)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **soft_post**
> Soft soft_post(body)

Create soft.

create soft

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
api_instance = aioalexandria.SoftApi(aioalexandria.ApiClient(configuration))
body = aioalexandria.SoftPostRequest() # SoftPostRequest | Post soft request

try:
    # Create soft.
    api_response = api_instance.soft_post(body)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling SoftApi->soft_post: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**SoftPostRequest**](SoftPostRequest.md)| Post soft request | 

### Return type

[**Soft**](Soft.md)

### Authorization

[Token](../README.md#Token)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

