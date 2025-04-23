Эти файлы автоматически сгенерированы с помощью [ts-proto][1]. Команда для генерации:

```
protoc \
  --plugin=./node_modules/.bin/protoc-gen-ts_proto \
  --ts_proto_out=./src \
  --ts_proto_opt=esModuleInterop=true,outputEncodeMethods=false,outputClientImpl=false,outputPartialMethods=false,useOptionals=true \
  -I $ARCADIA_ROOT/maps/doc/proto
  $ARCADIA_ROOT/maps/doc/proto/yandex/maps/proto/bizdir/{common,sps}/*.proto
```

Замечания:

* `protoc` нужен свежий, поэтому, если имеющийся в ОС не подходит, можно взять его в `.ya`
* Поскольку `ts-proto` так себе поддерживает опциональные поля с примитивными типами, то `verdict.ts` пропатчен вручную:
  - Все строки в вердиктах заменены на опциональные
  - `CompanyState` тоже сделан опциональным

[1]: https://github.com/stephenh/ts-proto
