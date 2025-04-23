# aioalexandria.MatcherApi

All URIs are relative to *http://localhost:9999/api/v1/*

Method | HTTP request | Description
------------- | ------------- | -------------
[**matcher_get**](MatcherApi.md#matcher_get) | **GET** /matcher/ | List matchers.
[**matcher_id_delete**](MatcherApi.md#matcher_id_delete) | **DELETE** /matcher/{id} | Delete matcher.
[**matcher_id_get**](MatcherApi.md#matcher_id_get) | **GET** /matcher/{id} | Get matcher.
[**matcher_post**](MatcherApi.md#matcher_post) | **POST** /matcher/ | Create matcher.

# **matcher_get**
> list[Matcher] matcher_get(only_model_re=only_model_re, only_rack_code=only_rack_code, category=category, rack_code=rack_code, model_re=model_re)

List matchers.

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
api_instance = aioalexandria.MatcherApi(aioalexandria.ApiClient(configuration))
only_model_re = 'only_model_re_example' # str | filter only model regexp matchers (optional)
only_rack_code = 'only_rack_code_example' # str | filter only rack code matchers (optional)
category = 'category_example' # str | filter by matcher category (optional)
rack_code = 'rack_code_example' # str | filter by exact rack code (optional)
model_re = 'model_re_example' # str | filter by exact model re (optional)

try:
    # List matchers.
    api_response = api_instance.matcher_get(only_model_re=only_model_re, only_rack_code=only_rack_code, category=category, rack_code=rack_code, model_re=model_re)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling MatcherApi->matcher_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **only_model_re** | **str**| filter only model regexp matchers | [optional] 
 **only_rack_code** | **str**| filter only rack code matchers | [optional] 
 **category** | **str**| filter by matcher category | [optional] 
 **rack_code** | **str**| filter by exact rack code | [optional] 
 **model_re** | **str**| filter by exact model re | [optional] 

### Return type

[**list[Matcher]**](Matcher.md)

### Authorization

[Token](../README.md#Token)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **matcher_id_delete**
> matcher_id_delete(id)

Delete matcher.

remove matcher

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
api_instance = aioalexandria.MatcherApi(aioalexandria.ApiClient(configuration))
id = 'id_example' # str | identifier of matcher

try:
    # Delete matcher.
    api_instance.matcher_id_delete(id)
except ApiException as e:
    print("Exception when calling MatcherApi->matcher_id_delete: %s\n" % e)
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

# **matcher_id_get**
> Matcher matcher_id_get(id)

Get matcher.

show matcher

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
api_instance = aioalexandria.MatcherApi(aioalexandria.ApiClient(configuration))
id = 'id_example' # str | identifier of matcher

try:
    # Get matcher.
    api_response = api_instance.matcher_id_get(id)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling MatcherApi->matcher_id_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **id** | **str**| identifier of matcher | 

### Return type

[**Matcher**](Matcher.md)

### Authorization

[Token](../README.md#Token)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **matcher_post**
> Matcher matcher_post(body)

Create matcher.

create matcher

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
api_instance = aioalexandria.MatcherApi(aioalexandria.ApiClient(configuration))
body = aioalexandria.MatcherPostRequest() # MatcherPostRequest | Matcher request

try:
    # Create matcher.
    api_response = api_instance.matcher_post(body)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling MatcherApi->matcher_post: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**MatcherPostRequest**](MatcherPostRequest.md)| Matcher request | 

### Return type

[**Matcher**](Matcher.md)

### Authorization

[Token](../README.md#Token)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

