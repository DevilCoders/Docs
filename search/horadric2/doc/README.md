# Here be dragons.

Документация максимально куцая и неточная. Да еще и на русском языке.  
Если знаешь где и как ее можно улучшить - смело открывай ревью или напиши [roboslone@](https://staff.yandex-team.ru/roboslone).


# Терминология
Все эти ваши дурацкие названия нормальным языком.  
За дурацкие названия тапки кидать в [roboslone@](https://staff.yandex-team.ru/roboslone).

### Scroll of Inifuss
Это всего лишь конфиг проекта.  
То что раньше называлось `horadric.conf` теперь называется `inifuss.scroll`.  
Протокол [тут](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/proto/internal/scroll.proto), пример свитка [тут](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/example/inifuss.scroll).

### Cairn Stones
Это кодогенераторы.  
Про них отдельно написано [тут](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/doc/cairn-stones.md).

### Inifuss
Это дерево протоколов - в нем собраны все protobuf-дескрипторы, которые доступны в проекте.  
Про него отдельно написано [тут](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/doc/inifuss.md).

### Rakanishu
Это маленький хелпер, который запускает кодогенерацию.  
Если ты не пишешь кодогенератор, то скорее всего не заметишь его.


# Flow
Как вообще вся эта фигня должна работать? ~~Наберут по объявлению...~~

Для начала надо в свитке написать какие именно протоколы нужны конкретному проекту.  
Делается это в поле `peers` - туда надо записать Аркадийные пути к `PROTO_LIBRARY`.

Дальше собери `search/horadric2/core` и запускай `cli/horadric`, передав ему путь к свитку и путь к корню Аркадии.  
Путь к корню Аркадии можно записать в переменную окружения `ARCADIA_ROOT`. Может когда-нибудь даже научимся находить его автоматически (сложно!).  
```bash
$ cd $ARCADIA_ROOT/search/horadric2/core
$ ya make -r --checkout
$ ./cli/horadric example/inifuss.scroll
```

CLI хорадрика сгенерирует [временный проект](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/doc/horadric-tmp.md) в `$ARCADIA_ROOT/junk/horadric-<project.name>`, там будет `ya.make`, `main.py` и стартап-скрипт для IPython.  
Если не передать в CLI `--do-not-make`, то временный проект будет собран (c `-r`).  
Если не передать в CLI `--do-not-run`, то будет запущена кодогенерация.  

Запустить кодогенерацию можно вручную, дернув `$ARCADIA_ROOT/junk/horadric-<project.name>/horadric-temp`.  
Можно запустить IPython в контексте временного проекта (со всеми протоколами и core-библиотекой самого хорадрика), добавив к `horadric-temp` ключик `-i`.  

В IPython будут доступны переменные `scroll`, `inifuss` и `rakanishu`.  
Запустить кодогенерацию из IPython можно так: `rakanishu.activate_cairn_stones()`.  

Дальше при разработке камня можно пересобирать и перезапускать только `horadric-temp`.  
