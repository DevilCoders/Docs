# aioalexandria.ModelInfoMatcherApi

All URIs are relative to *http://localhost:9999/api/v1/*

Method | HTTP request | Description
------------- | ------------- | -------------
[**model_info_matcher_get**](ModelInfoMatcherApi.md#model_info_matcher_get) | **GET** /model_info_matcher/ | List model info matchers.
[**model_info_matcher_id_delete**](ModelInfoMatcherApi.md#model_info_matcher_id_delete) | **DELETE** /model_info_matcher/{id} | Delete model info matcher.
[**model_info_matcher_id_get**](ModelInfoMatcherApi.md#model_info_matcher_id_get) | **GET** /model_info_matcher/{id} | Get model info matcher.
[**model_info_matcher_post**](ModelInfoMatcherApi.md#model_info_matcher_post) | **POST** /model_info_matcher/ | Create model info matcher.

# **model_info_matcher_get**
> list[ModelInfoMatcher] model_info_matcher_get(only_model_re=only_model_re, only_rack_code=only_rack_code, rack_code=rack_code, model_re=model_re, soft_ids=soft_ids)

List model info matchers.

show matchers list

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
api_instance = aioalexandria.ModelInfoMatcherApi(aioalexandria.ApiClient(configuration))
only_model_re = 'only_model_re_example' # str | filter only model regexp matchers (optional)
only_rack_code = 'only_rack_code_example' # str | filter only rack code matchers (optional)
rack_code = 'rack_code_example' # str | filter by exact rack code (optional)
model_re = 'model_re_example' # str | filter by exact model re (optional)
soft_ids = ['soft_ids_example'] # list[str] | filter by soft ids (optional)

try:
    # List model info matchers.
    api_response = api_instance.model_info_matcher_get(only_model_re=only_model_re, only_rack_code=only_rack_code, rack_code=rack_code, model_re=model_re, soft_ids=soft_ids)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling ModelInfoMatcherApi->model_info_matcher_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **only_model_re** | **str**| filter only model regexp matchers | [optional] 
 **only_rack_code** | **str**| filter only rack code matchers | [optional] 
 **rack_code** | **str**| filter by exact rack code | [optional] 
 **model_re** | **str**| filter by exact model re | [optional] 
 **soft_ids** | [**list[str]**](str.md)| filter by soft ids | [optional] 

### Return type

[**list[ModelInfoMatcher]**](ModelInfoMatcher.md)

### Authorization

[Token](../README.md#Token)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **model_info_matcher_id_delete**
> model_info_matcher_id_delete(id)

Delete model info matcher.

remove model info matcher

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
api_instance = aioalexandria.ModelInfoMatcherApi(aioalexandria.ApiClient(configuration))
id = 'id_example' # str | identifier of matcher

try:
    # Delete model info matcher.
    api_instance.model_info_matcher_id_delete(id)
except ApiException as e:
    print("Exception when calling ModelInfoMatcherApi->model_info_matcher_id_delete: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **id** | **str**| identifier of matcher | 

### Return type

void (empty response body)

### Authorization

[Token](../README.md#Token)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **model_info_matcher_id_get**
> ModelInfoMatcher model_info_matcher_id_get(id)

Get model info matcher.

show model info matcher

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
api_instance = aioalexandria.ModelInfoMatcherApi(aioalexandria.ApiClient(configuration))
id = 'id_example' # str | identifier of model info matcher

try:
    # Get model info matcher.
    api_response = api_instance.model_info_matcher_id_get(id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling ModelInfoMatcherApi->model_info_matcher_id_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **id** | **str**| identifier of model info matcher | 

### Return type

[**ModelInfoMatcher**](ModelInfoMatcher.md)

### Authorization

[Token](../README.md#Token)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **model_info_matcher_post**
> ModelInfoMatcher model_info_matcher_post(body)

Create model info matcher.

create model info matcher

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
api_instance = aioalexandria.ModelInfoMatcherApi(aioalexandria.ApiClient(configuration))
body = aioalexandria.ModelInfoMatcherPostRequest() # ModelInfoMatcherPostRequest | ModelInfoMatcher request

try:
    # Create model info matcher.
    api_response = api_instance.model_info_matcher_post(body)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling ModelInfoMatcherApi->model_info_matcher_post: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**ModelInfoMatcherPostRequest**](ModelInfoMatcherPostRequest.md)| ModelInfoMatcher request | 

### Return type

[**ModelInfoMatcher**](ModelInfoMatcher.md)

### Authorization

[Token](../README.md#Token)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

