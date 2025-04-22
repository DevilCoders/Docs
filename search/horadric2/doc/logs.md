# Логи
## Где логи? В выхлопе (почти) ничего нет!
Спокойно, вместо логов нынче [трейсы](https://a.yandex-team.ru/arc/trunk/arcadia/search/martylib/trace).  
Пишутся они в файлики с расширением `.blog`. Прочитать можно, например, [dummy-parser](https://a.yandex-team.ru/arc/trunk/arcadia/search/martylib/trace/parser/dummy/ya.make)'ом:
```bash
$ alias parser="$ARCADIA_ROOT/search/martylib/trace/parser/dummy/dummy-parser"
$ parser $ARCADIA_ROOT/junk/horadric-example/horadric-temp.blog
```
