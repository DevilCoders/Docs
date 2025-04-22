# solomon_client.SensorsApi

All URIs are relative to *//solomon.yandex-team.ru/*

Method | HTTP request | Description
------------- | ------------- | -------------
[**find_all_label_values_in_old_format_using_get**](SensorsApi.md#find_all_label_values_in_old_format_using_get) | **GET** /api/v2/projects/{projectId}/sensors/labels | find all label values by selector query
[**find_label_keys_in_old_format_using_get**](SensorsApi.md#find_label_keys_in_old_format_using_get) | **GET** /api/v2/projects/{projectId}/sensors/names | find label names by selector query
[**find_metric_names_using_get**](SensorsApi.md#find_metric_names_using_get) | **GET** /api/v2/projects/{projectId}/sensors/sensorNames | find all sensor names in project
[**find_sensors_using_get**](SensorsApi.md#find_sensors_using_get) | **GET** /api/v2/projects/{projectId}/sensors | find sensors by selector query

# **find_all_label_values_in_old_format_using_get**
> LabelValuesResponseDto find_all_label_values_in_old_format_using_get(project_id, validation_filter=validation_filter, force_cluster=force_cluster, limit=limit, names=names, selectors=selectors, text=text, use_new_format=use_new_format)

find all label values by selector query

This action returns values of label by selector query if user have permissions to read that project.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.SensorsApi()
project_id = 'project_id_example' # str | projectId
validation_filter = 'ALL' # str | label validation filter (internal parameter, will be removed) (optional) (default to ALL)
force_cluster = 'force_cluster_example' # str | force cluster parameter (dc abbreviation or empty) (optional)
limit = solomon_client.Ref() # Ref | label values count limit [0; 100000] (optional)
names = 'names_example' # str | list of required label names joining by comma, leave it empty to show all label names (optional)
selectors = 'selectors_example' # str | selector query (optional)
text = 'text_example' # str | case insensitive text filter by labels (optional)
use_new_format = true # bool | use new selector query format (optional)

try:
    # find all label values by selector query
    api_response = api_instance.find_all_label_values_in_old_format_using_get(project_id, validation_filter=validation_filter, force_cluster=force_cluster, limit=limit, names=names, selectors=selectors, text=text, use_new_format=use_new_format)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling SensorsApi->find_all_label_values_in_old_format_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **project_id** | **str**| projectId | 
 **validation_filter** | **str**| label validation filter (internal parameter, will be removed) | [optional] [default to ALL]
 **force_cluster** | **str**| force cluster parameter (dc abbreviation or empty) | [optional] 
 **limit** | [**Ref**](.md)| label values count limit [0; 100000] | [optional] 
 **names** | **str**| list of required label names joining by comma, leave it empty to show all label names | [optional] 
 **selectors** | **str**| selector query | [optional] 
 **text** | **str**| case insensitive text filter by labels | [optional] 
 **use_new_format** | **bool**| use new selector query format | [optional] 

### Return type

[**LabelValuesResponseDto**](LabelValuesResponseDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **find_label_keys_in_old_format_using_get**
> LabelNamesResponseDto find_label_keys_in_old_format_using_get(project_id, force_cluster=force_cluster, selectors=selectors, use_new_format=use_new_format)

find label names by selector query

This action returns label names by selector query if user have permissions to read that project.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.SensorsApi()
project_id = 'project_id_example' # str | projectId
force_cluster = 'force_cluster_example' # str | force cluster parameter (dc abbreviation or empty) (optional)
selectors = 'selectors_example' # str | selector query (optional)
use_new_format = true # bool | use new selector query format (optional)

try:
    # find label names by selector query
    api_response = api_instance.find_label_keys_in_old_format_using_get(project_id, force_cluster=force_cluster, selectors=selectors, use_new_format=use_new_format)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling SensorsApi->find_label_keys_in_old_format_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **project_id** | **str**| projectId | 
 **force_cluster** | **str**| force cluster parameter (dc abbreviation or empty) | [optional] 
 **selectors** | **str**| selector query | [optional] 
 **use_new_format** | **bool**| use new selector query format | [optional] 

### Return type

[**LabelNamesResponseDto**](LabelNamesResponseDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **find_metric_names_using_get**
> MetricNamesResponseDto find_metric_names_using_get(project_id, validation_filter=validation_filter, force_cluster=force_cluster, limit=limit, selectors=selectors, text=text)

find all sensor names in project

This action returns sensor names in project if user have permissions to read that project.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.SensorsApi()
project_id = 'project_id_example' # str | projectId
validation_filter = 'ALL' # str | label validation filter (internal parameter, will be removed) (optional) (default to ALL)
force_cluster = 'force_cluster_example' # str | force cluster parameter (dc abbreviation or empty) (optional)
limit = solomon_client.Ref() # Ref | metric names count limit [0; 100000] (optional)
selectors = 'selectors_example' # str | selector query (optional)
text = 'text_example' # str | case insensitive text filter by labels (optional)

try:
    # find all sensor names in project
    api_response = api_instance.find_metric_names_using_get(project_id, validation_filter=validation_filter, force_cluster=force_cluster, limit=limit, selectors=selectors, text=text)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling SensorsApi->find_metric_names_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **project_id** | **str**| projectId | 
 **validation_filter** | **str**| label validation filter (internal parameter, will be removed) | [optional] [default to ALL]
 **force_cluster** | **str**| force cluster parameter (dc abbreviation or empty) | [optional] 
 **limit** | [**Ref**](.md)| metric names count limit [0; 100000] | [optional] 
 **selectors** | **str**| selector query | [optional] 
 **text** | **str**| case insensitive text filter by labels | [optional] 

### Return type

[**MetricNamesResponseDto**](MetricNamesResponseDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **find_sensors_using_get**
> PagedResultDtoMetricDto find_sensors_using_get(project_id, force_cluster=force_cluster, selectors=selectors, use_new_format=use_new_format)

find sensors by selector query

This action returns project's sensors by selector query if user have permissions to read that project.

### Example
```python
from __future__ import print_function
import time
import solomon_client
from solomon_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = solomon_client.SensorsApi()
project_id = 'project_id_example' # str | projectId
force_cluster = 'force_cluster_example' # str | force cluster parameter (optional)
selectors = 'selectors_example' # str | selector query (optional)
use_new_format = true # bool | use new selector query format (optional)

try:
    # find sensors by selector query
    api_response = api_instance.find_sensors_using_get(project_id, force_cluster=force_cluster, selectors=selectors, use_new_format=use_new_format)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling SensorsApi->find_sensors_using_get: %s\n" % e)
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **project_id** | **str**| projectId | 
 **force_cluster** | **str**| force cluster parameter | [optional] 
 **selectors** | **str**| selector query | [optional] 
 **use_new_format** | **bool**| use new selector query format | [optional] 

### Return type

[**PagedResultDtoMetricDto**](PagedResultDtoMetricDto.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json;charset=UTF-8

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

