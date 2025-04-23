# Cairn Stones

## Кто такой, чем знаменит?
**Cairn Stones** (камни, камушки) - это кодогенераторы.
Специальная штуковина [Rakanishu](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/doc/rakanishu.md) активирует камушки для конкретного проекта, чтобы они что-нибудь сгенерировали. Что именно - само собой, зависит от конкретного камушка.

## Как написать?
Камушек, по сути, это питонячий класс, отнаследованный от [CairnStone](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/core/rakanishu/cairn_stone.py).
Переопределить, фактически, нужно только метод `activate`.  
Пишутся они как `PY3_LIBRARY`.  

Что произойдет после активации камня - одному автору известно (потому что чисто теоретически произойти может что угодно).  
Однако ожидается, что камень сгенерирует какой-то код. Собирать его не будет и запускать тоже.  

## Примеры? Их есть у меня.  
Вот, к слову, камешек знаний ([KnowledgeStone](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/core/cairn_stones/knowledge/__init__.py)). Он существует исключительно в целях демонстрации возможностей `horadric` и генерирует Markdown с описанием найденных протоколов (сервисов, сообщений и enum'ов). Сгенерированное попадает в директорию проекта, в папочку `doc`.  

Поштырим в код?  

Прямо при инициализации камушек [чистит директорию](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/core/cairn_stones/knowledge/__init__.py?rev=5014629#L23) с "документацией" (так себе подход, если честно).  

Дальше он ждет пока его активируют.  

Сразу при активации он забирает из [Inifuss](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/doc/inifuss.md) все enum'ы, сообщения и сервисы, которые имеют отношения к конкретному peer'у (peer'ы задаются отдельно для каждого проекта в [свитке](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/doc/scroll.md)).  

Потом проходится по этим прекрасным сущностям и из jinja-шаблонов [генерирует какой-то Markdown-текст](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/core/cairn_stones/knowledge/__init__.py?rev=5014629#L64), который после [записывает в файлик](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/core/cairn_stones/knowledge/__init__.py?rev=5014629#L73).  

Вот, собственно, и все.  
Вот [тут](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/core/cairn_stones/shadow/__init__.py) можно почитать про камушек посложнее.

## Ну ладно, написал, дальше что? Как использовать в свитках, как поделиться с общественностью?
Камушек надо показать [Rakanishu](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/doc/rakanishu.md). Делается это вот [тут](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/core/rakanishu/rakanishu.py?rev=5015984#L24).  
Перед этим неплохо бы добавить его в `PEERDIR` - [тут](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/core/ya.make?rev=5015984#L29).  
Еще можно робко надеяться, что Rakanishu сам найдет все существующие камни, но такого он пока не умеет.

## Шеф, все пропало! Как это дебажить?!
Тут два варианта - IPython и логи.
Про логи написано [тут](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/doc/logs.md), про запуск IPython - [тут](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/doc/README.md#flow).  
Пример запуска камешка из IPython:  
```bash
$ cd $ARCADIA_ROOT/junk/horadric-example
$ ./horadric-tmp -i
```
```python
from search.horadric2.core.cairn_stones.shadow import ShadowStone

stone = ShadowStone(rakanishu, args='')
stone.activate(scroll.peers[0])
```
