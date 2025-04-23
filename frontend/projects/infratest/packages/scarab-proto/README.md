# Scarab proto

Пакет, содержащий сериализатор/десериализатор для сущностей `scarab`, а так же тайпинги к ним.

Прото-схемы можно посмотреть [тут](https://a.yandex-team.ru/arcadia/scarab/api/proto).

Пример использования:
```
import { NScarabProto } from "../generated";
const { NReport: { TWebReportSearchReqansEvent } } = NScarabProto;

const reqans = TWebReportSearchReqansEvent.create({
    RequestId: "reqId",
});
```
