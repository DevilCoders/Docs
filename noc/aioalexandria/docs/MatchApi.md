# aioalexandria.MatchApi

All URIs are relative to *http://localhost:9999/api/v1/*

Method | HTTP request | Description
------------- | ------------- | -------------
[**match_bulk_post**](MatchApi.md#match_bulk_post) | **POST** /match/bulk/ | Show matches for a lot of models, objects, fqdns.
[**match_get**](MatchApi.md#match_get) | **GET** /match/ | Show matched softs for model.

# **match_bulk_post**
> BulkMatchResponse match_bulk_post(body)

Show matches for a lot of models, objects, fqdns.

get matches for a lot of models, objects, fqdns.

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
api_instance = aioalexandria.MatchApi(aioalexandria.ApiClient(configuration))
body = aioalexandria.BulkMatchRequest() # BulkMatchRequest | Bulk match request

try:
    # Show matches for a lot of models, objects, fqdns.
    api_response = api_instance.match_bulk_post(body)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling MatchApi->match_bulk_post: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**BulkMatchRequest**](BulkMatchRequest.md)| Bulk match request | 

### Return type

[**BulkMatchResponse**](BulkMatchResponse.md)

### Authorization

[Token](../README.md#Token)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **match_get**
> Match match_get(model=model, fqdn=fqdn, object_id=object_id, category=category)

Show matched softs for model.

get matched softs for model

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
api_instance = aioalexandria.MatchApi(aioalexandria.ApiClient(configuration))
model = 'model_example' # str | Model (optional)
fqdn = 'fqdn_example' # str | FQDN (optional)
object_id = 56 # int | RT Object ID (optional)
category = 'category_example' # str | filter by matcher category (optional)

try:
    # Show matched softs for model.
    api_response = api_instance.match_get(model=model, fqdn=fqdn, object_id=object_id, category=category)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling MatchApi->match_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **model** | **str**| Model | [optional] 
 **fqdn** | **str**| FQDN | [optional] 
 **object_id** | **int**| RT Object ID | [optional] 
 **category** | **str**| filter by matcher category | [optional] 

### Return type

[**Match**](Match.md)

### Authorization

[Token](../README.md#Token)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

