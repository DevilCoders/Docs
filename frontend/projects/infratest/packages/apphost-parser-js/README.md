# Apphost-parser-js

Библиотека для парсинга apphost-запросов почти на чистом js. Для распаковки используются компилируемые либы.

Пока поддерживается только протокол NEH. Не поддерживается стриминг.

## Использование

```javascript
import { ApphostIncomingContext, ApphostOutgoingContext, cleanProtoObject } from "@yandex-int/apphost-parser-js";

const inCtx = new ApphostIncomingContext(body);
const request = inCtx.getItems("request")[0];
const protoItem = inCtx.getProtobufItems("proto_item")[0];
if (inCtx.hasFlag("input flag")) {
    console.log("Flag was set");
}

const outCtx = new ApphostOutgoingContext();
outCtx.addItem("log_reqans", "item value goes here"); 
outCtx.addProtobufItem("proto_item_cleaned", MessageClass.encode(cleanProtoObject({ Key1: 0, Key2: "Hello" })).finish()); 
outCtx.addFlag("some flag name");
outCtx.setException(Buffer.from("some error message"));
outCtx.addLogLine(Buffer.from("some log line"));
```

Библиотека экспортирует:

- `ApphostIncomingContext`
- `ApphostOutgoingContext`
- `cleanProtoObject`ar - функция-хэлпер для уменьшения количества пересылаемых данных. Очищает объект от полей, в которых содержатся значения по умолчанию.  
- `NApphostHttp` - скомпилированные типы [http-айтемов apphost](https://a.yandex-team.ru/arc/trunk/arcadia/apphost/lib/proto_answers/http.proto).
