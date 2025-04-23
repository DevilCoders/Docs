geobase
=======

Hack the user by their IP address, add the location as `x-region-*` request headers. See [the documentation for LaaS](https://doc.yandex-team.ru/laas/laas-user/concepts/balancer_headers.html), the underlying service.

Syntax
------

```yaml
- geobase: geobase-action
```

Options
-------

**(argument)**: an action that implements the LaaS API: accepts a GET to the specified path and returns the result in the response headers.

**path** (default=`/region?response_format=header&version=1&service=balancer`): the path to use when requesting data from LaaS. Must use the header response format.

**trusted** (default=false): whether to use existing `x-region-*` headers in the request, if present, instead of sending a request to LaaS.

Signals
-------

**trusted_dmmm**: when `trusted` is true, the number of requests with their own values of `x-region-*`.

**no-ip-header_dmmm**: the number of requests that have not been augmented with region information because of a missing `x-forwarded-for-y` header.

**no-region_dmmm**: the number of requests for which LaaS has provided no region information.
