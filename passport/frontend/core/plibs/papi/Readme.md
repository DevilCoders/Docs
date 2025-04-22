```javascript

//Initialize the data access object
var HttpDao = require('pdao/Http');
var dao = new HttpDao(
	logID,
    daoConfig.baseUrl,
    daoConfig.maxRetries,
    daoConfig.retryAfter,
    daoConfig.maxConnections,
    daoConfig.timeout,
    require('papi/OAuth/retryCondition')(daoConfig.retryCodes)
);

//Initialize the api
var OAuthApi = require('papi/OAuth');
var oauthApi = new OAuthApi(logID, dao, lang);

//Call the api method
oauthApi.visibleScopes();
```
