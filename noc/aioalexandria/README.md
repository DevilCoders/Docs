# aioalexandria
This is a default soft server.

This Python package is automatically generated by the [Swagger Codegen](https://github.com/swagger-api/swagger-codegen) project:

- API version: 1.0
- Package version: 1.0.0
- Build package: io.swagger.codegen.v3.generators.python.PythonClientCodegen
For more information, please visit [https://a.yandex-team.ru/arc/trunk/arcadia/noc/alexandria/](https://a.yandex-team.ru/arc/trunk/arcadia/noc/alexandria/)

## Requirements.

Python 2.7 and 3.4+

## Installation & Usage
### pip install

If the python package is hosted on Github, you can install directly from Github

```sh
pip install git+https://github.com/nocdev/aioalexandria.git
```
(you may need to run `pip` with root permission: `sudo pip install git+https://github.com/nocdev/aioalexandria.git`)

Then import the package:
```python
import aioalexandria 
```

### Setuptools

Install via [Setuptools](http://pypi.python.org/pypi/setuptools).

```sh
python setup.py install --user
```
(or `sudo python setup.py install` to install the package for all users)

Then import the package:
```python
import aioalexandria
```

## Getting Started

Please follow the [installation procedure](#installation--usage) and then run the following:

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

## Documentation for API Endpoints

All URIs are relative to *http://localhost:9999/api/v1/*

Class | Method | HTTP request | Description
------------ | ------------- | ------------- | -------------
*MatchApi* | [**match_bulk_post**](docs/MatchApi.md#match_bulk_post) | **POST** /match/bulk/ | Show matches for a lot of models, objects, fqdns.
*MatchApi* | [**match_get**](docs/MatchApi.md#match_get) | **GET** /match/ | Show matched softs for model.
*MatcherApi* | [**matcher_get**](docs/MatcherApi.md#matcher_get) | **GET** /matcher/ | List matchers.
*MatcherApi* | [**matcher_id_delete**](docs/MatcherApi.md#matcher_id_delete) | **DELETE** /matcher/{id} | Delete matcher.
*MatcherApi* | [**matcher_id_get**](docs/MatcherApi.md#matcher_id_get) | **GET** /matcher/{id} | Get matcher.
*MatcherApi* | [**matcher_post**](docs/MatcherApi.md#matcher_post) | **POST** /matcher/ | Create matcher.
*ModelInfoApi* | [**model_info_get**](docs/ModelInfoApi.md#model_info_get) | **GET** /model_info/ | List model info.
*ModelInfoApi* | [**model_info_id_delete**](docs/ModelInfoApi.md#model_info_id_delete) | **DELETE** /model_info/{id} | Delete model info.
*ModelInfoApi* | [**model_info_id_get**](docs/ModelInfoApi.md#model_info_id_get) | **GET** /model_info/{id} | Get model info.
*ModelInfoApi* | [**model_info_post**](docs/ModelInfoApi.md#model_info_post) | **POST** /model_info/ | Create model info.
*ModelInfoMatcherApi* | [**model_info_matcher_get**](docs/ModelInfoMatcherApi.md#model_info_matcher_get) | **GET** /model_info_matcher/ | List model info matchers.
*ModelInfoMatcherApi* | [**model_info_matcher_id_delete**](docs/ModelInfoMatcherApi.md#model_info_matcher_id_delete) | **DELETE** /model_info_matcher/{id} | Delete model info matcher.
*ModelInfoMatcherApi* | [**model_info_matcher_id_get**](docs/ModelInfoMatcherApi.md#model_info_matcher_id_get) | **GET** /model_info_matcher/{id} | Get model info matcher.
*ModelInfoMatcherApi* | [**model_info_matcher_post**](docs/ModelInfoMatcherApi.md#model_info_matcher_post) | **POST** /model_info_matcher/ | Create model info matcher.
*SoftApi* | [**soft_get**](docs/SoftApi.md#soft_get) | **GET** /soft/ | List soft.
*SoftApi* | [**soft_id_delete**](docs/SoftApi.md#soft_id_delete) | **DELETE** /soft/{id} | Delete soft.
*SoftApi* | [**soft_id_get**](docs/SoftApi.md#soft_id_get) | **GET** /soft/{id} | Get soft.
*SoftApi* | [**soft_post**](docs/SoftApi.md#soft_post) | **POST** /soft/ | Create soft.

## Documentation For Models

 - [APIError](docs/APIError.md)
 - [BulkMatchRequest](docs/BulkMatchRequest.md)
 - [BulkMatchResponse](docs/BulkMatchResponse.md)
 - [Match](docs/Match.md)
 - [Matcher](docs/Matcher.md)
 - [MatcherPostRequest](docs/MatcherPostRequest.md)
 - [ModelInfo](docs/ModelInfo.md)
 - [ModelInfoMatcher](docs/ModelInfoMatcher.md)
 - [ModelInfoMatcherPostRequest](docs/ModelInfoMatcherPostRequest.md)
 - [ModelInfoPostRequest](docs/ModelInfoPostRequest.md)
 - [Soft](docs/Soft.md)
 - [SoftPostRequest](docs/SoftPostRequest.md)

## Documentation For Authorization


## Token

- **Type**: API key
- **API key parameter name**: Authorization
- **Location**: HTTP header


## Author

noc-dev@yandex-team.ru
