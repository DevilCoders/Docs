# TPbArgEntryPoint

Объединяет `library/cpp/getoptpb` и использование json конфига.

Использование:
```cpp
// ...

int Main(const TSomeConfProto& conf) {
    // ...
}

int main(int argc, const char** argv) {
    return TPbArgEntryPoint::RunPbArgMain(&Main, argc, argv);
}
```

Где `TSomeConfProto` может выглядеть так:

```proto
message TSomeConfProto {
    option (NGetoptPb.Title) = "Some description";

    required string ConfigFile = 1 [
        default = "",
        (NGetoptPb.Conf) = {
            Descr: "Json config from this file will be read and merged with this config, that is parsed from command line arguments (this config is higher priority). Use only this option if you are not debugging."
            Short: 'c'
        }];

    optional uint32 VerboseLevel = 2 [default = 6];
    optional string GlobalLog = 3 [default = "cerr"];

    // ...
};
```

Аргументы командной строки парсятся с помощью `library/cpp/getoptpb`.
Если в протобуфе есть поле `string ConfigFile`, то оно понимается как имя файла с json-конфигом,
этот конфиг подргужается, превращается в протобуф и этот протобуф мерджится с протобуфом полученным из аргументов командной строки.
То есть опции идут в первую очередь из аргументов программы, во вторую - из json-конфига.
