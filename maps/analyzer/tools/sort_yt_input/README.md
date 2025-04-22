Сортировка входных данных в YSON
===

### Использование

```bash
cat input.yson | ./bin/sort_yt_input --sort-by clid --sort-by uuid --sort-by enter_time > sorted.yson
```

См. также [`generate_yt_binary_input`](/arc/trunk/arcadia/maps/analyzer/tools/generate_yt_binary_input).

### Ограничения

Сортирует просто формированием кортежа по указанным колонкам, из-за чего может не учитывать специфику сортировки YT, но для простых типов должно работать.
