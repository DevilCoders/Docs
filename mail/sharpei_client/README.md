## Sharpei client

C++ library over the Sharpei [REST API](https://wiki.yandex-team.ru/mail/pg/sharpei/interface/mail/).

The C++ interface is [here](https://a.yandex-team.ru/arc/trunk/arcadia/mail/sharpei_client/include/sharpei_client/sharpei_client.h?rev=r8996573#L93).

[Settings](https://a.yandex-team.ru/arc/trunk/arcadia/mail/sharpei_client/include/sharpei_client/sharpei_client.h?rev=r8996573#L16) should be parsed using the provided [helper method](https://a.yandex-team.ru/arc/trunk/arcadia/mail/sharpei_client/include/sharpei_client/integration.h?rev=r8996573#L13).

### How to use

#### The new factory
Easier to use due to the native integration with `yhttp::cluster_client`.

In order to create a `SharpeiClient`, you have to provide **only** the following fields of the settings:
- `settings.httpClient->clusterClientModuleName` - name of the `yhttp::cluster_client` module

The other fields **must** be left empty.

Also you have to properly configure `yhttp::cluster_client` itself. \
In order to do it correctly, please **refer to the [docs](https://a.yandex-team.ru/arc/trunk/arcadia/mail/ymod_httpclient)**. \
The following is a brief description of the correspondence between the `sharpei::client::Settings` fields and the `yhttp::cluster_client` setings:
```yaml
nodes: [ 'http://sharpei-production.mail.yandex.net:80' ] # equivalent of <host>/<port> in original settings
connect_attempt_timeout: 0.3s  # equivalent of <timeout>
default_request_timeout: 0.3s  # equivalent of <timeout>
reuse_connection: 0 # equivalent of <keep_alive>
retry_policy:
    max_attempts: 3 # equivalent of <retries>
```

The factory signature is:

```cpp
SharpeiClientPtr createSharpeiClient(const Settings& settings, const RequestInfo& requestInfo);
```

#### The old one
Uses a user provided implementation of the [HttpClient](https://a.yandex-team.ru/arc/trunk/arcadia/mail/sharpei_client/include/sharpei_client/http.h?rev=r8996573#L41).

The factory signature is:

```cpp
SharpeiClientPtr createSharpeiClient(http::HttpClientPtr httpClient, const Settings& settings, const RequestInfo& requestInfo);
```
