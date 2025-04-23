# Apphost http proto
Пакет, содержащий сериализатор/десериализатор для аппхостовых ```http_request``` и ```http_response```, а так же тайпинги к ним.

Прото-схемы можно посмотреть [тут](https://a.yandex-team.ru/arc_vcs/apphost/lib/proto_answers/http.proto).

Пример использования:
```
import { NAppHostHttp } from "@yandex-int/apphost-http-proto";

const request = NAppHostHttp.THttpRequest.create({ Path: '/search' });
```
