## Вспомогательные функции
### url_encode и form_encode
```
#include <ymod_httpclient/url_encode.h>

auto request = yhttp::request::POST("/path" +
    yhttp::url_encode {
        {"param","value"},
        {"param","value"}},
    yhttp::form_encode {
        {"bodyparam", "value"}
    });
```

