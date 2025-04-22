# TGeneratedBanner

В этот протобуф можно добавлять только поля элементарных типов (`uint64`, `int64`, `string`, `bytes` итд), нельзя добавлять другие message как типы, то есть следующее запрещено:

```proto
message FormalAge {
    // ...
}

// ...

optional FormalAge AgeNew = 72    [(NYT.column_name) = "AgeNew", json_name="AgeNew"];
//       ^^^^^^^^^ запрещено
```

Запрещено, потому что это отправляется в CaeSaR, а он ожидает либо простой тип данных, либо Yson (YtNode). Если вы не последуете этой инструкции, то можете получать ошибки вида `(yexception) library/cpp/protobuf/yt/yt2proto.cpp:274: expected map node`.

В случае если хочется складывать структурированные данные, нужно делать это следующим образом:
* Тип - `bytes`
* В квадратных скобках в объявлении поля указано `(NYT.flags) = ANY`
* В коде поле складывается в `TGeneratedBanner` следующим образом:
```c++
FormalAge ageNew;
// ...
banner->SetAgeNew(NYT::NodeToYsonString(ProtoToYtNode(ageNew)));
```
* В коде поле достаётся из `TGeneratedBanner` следующим образом:
```c++
FormalAge ageNew;
YtNodeToProto(NYT::NodeFromYsonString(banner.GetAgeNew()), ageNew);
```