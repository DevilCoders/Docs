# Typed http getter
It's almost the same `http_getter` but based on `yhttp::typed_client`. \
Which leads to more efficient retries and ability to use retry strategies.

## TypedClient
Provides `toGET/.../toDELETE` methods which convert a builder to a request. \
Also applies tvm ticket(s) and passes headers to request.

## TypedEndpoint
Description of a http resource: `method`, `tmv_service`, `log_response_body`, `client` (aka executor). \
Most of options are moved from endpoint to it's `client`. \
See an example:
```yaml
some_endpoint:
    method: /api/mailbox_list
    tvm_service: some_service_with_description_in_tvm_section
    log_response_body: true
    client:
        reactor: some_reactor # Note: this is required
        enable_logging: true
        tskv_logging: true
        tskv_log_name: 'http_client'
        reuse_connection: false
        nodes: [locahost:8080, fallback:8081]
        default_request_timeout: 1s
        retry_policy:
            split_timeout: true # Note: this is important
            max_attempts: 3
            codes: [500, 501, 502, 503, 504]
```
All available settings for `client` section are [here](https://a.yandex-team.ru/arc_vcs/mail/ymod_httpclient/doc/cluster_client).

`format(...)` applies arguments to `method` and returns new copy of endpoint.

### Timeouts

**Note**: `split_timeout`: without setting this parameter all amount of `default_request_timeout` will be spent on the **1st** attempt. \
With this parameter set the split is like that:
- 1st attempt will get `default_request_timeout/2` e.g., `500ms`
- rest will get the remaining equally e.g., \
`(default_request_timeout - (default_request_timeout / 2)) / (max_attempts - 1)` \
` = (1s - 500ms)/2 = 250ms` per request. \
Because we have 3 attempts here.

Because of this timeouts are differ in the typed version. \
For example in the old version you have:
```yaml
endpoint:
    # ...
    timeout_ms:
        connect: 200
        total: 2000
    tries: 3
```
Then in the new one you have to do something like that:

```yaml
endpoint:
    # ...
    client:
        # ...
        connect_attempt_timeout: 200ms
        default_request_timeout: 6s
        retry_policy:
            max_attempts: 3
```
And in this case: **1st** attempt gets `3s`, **2nd** and **3rd** get `1.5s` each.


## Handler and retries
As far as underlying http client is able to retry requests itself there are several options:
- specify retry codes in `retry_policy.codes` and these codes will be retried without calling your `handler`
- manage retry by codes in your `handler`

Also an intersection of these options is possible, for example:
- `retry_policy.codes=[500, 501]`
- and `handler` is
```cpp
const auto handler = [&] (yhttp::response resp) {
    if (http_getter::helpers::successCode(resp.status)) {
        return http_getter::Result::success;
    }
    return http_getter::Result::retry;
};
```
In this case some part of requests will directed to retry by `retry_policy.codes` and another by `handler`.


## Logging

Logging is pretty the same. \
**But there is a nuance**: in case if a retry is made by `retry_policy.codes`, your logger will not be executed and will not know about this retry.

Stay tuned)
