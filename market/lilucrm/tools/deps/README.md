# Парсер и визуализатор дерева зависимостей
## Парсер - parse_deps.py
Разбирает дерево зависимостей, генерируемое с помощью
```sh
ya java dependency-tree
```

**Вызов:**
```sh
./parse_deps.py [file]
```
Если `file` не задан, то читает со стандартного ввода.
Печатает на стандартный вывод JSON вида:
```javascript
{
    "nodes": ["node1", "node2", ...],
    "links": [["node1", "node2"], ...]
}
```

**Пример:**
```sh
mkdir -p tmp
<example.deps.txt ./parse_deps_tree.py >tmp/example.deps.json
```
## Визуализатор - deps2dot.py
Генерирует `*.dot` файл для графа зависимостей в JSON формате, возвращаемом `parse_deps.py`.

**Вызов:**
```shell
./deps2dot.py [file]
```
Если `file` не задан, то читает со стандартного ввода JSON с графом зависимостей.
Печатает на стандартный вывод `*.dot` файл для визуализации этого графа. 

**Пример:**
```shell
./deps2dot.py tmp/example.deps.json >tmp/example.deps.dot
dot -Tsvg tmp/example.deps.dot >tmp/example.deps.svg
```

## Ограничение графа зависимостей
### restrict_deps.py
Позволяет ограничить граф определённой поддиректорией или несколькими.
**Вызов:**
```sh
./restrict_deps.py path ...
```
Читает со стандартного ввода JSON с графом и выводит новый,
ограниченный заданными поддиректориями.

### remove_nodes.py
Удаляет из графа зависимостей набор узлов.
**Вызов:**
```sh
./remove_nodes.py node ...
```
Читает со стандартного ввода JSON с графом и выводит новый,
без заданных узлов.

### transitive_reduction.py
Выполняет [Транзитивное сокращение](https://ru.wikipedia.org/wiki/%D0%A2%D1%80%D0%B0%D0%BD%D0%B7%D0%B8%D1%82%D0%B8%D0%B2%D0%BD%D0%BE%D0%B5_%D1%81%D0%BE%D0%BA%D1%80%D0%B0%D1%89%D0%B5%D0%BD%D0%B8%D0%B5).
Печатает удалённые связи на stderr.

## Установка зависимостей
```sh
make init
```

## Запуск тестов
```sh
make test
```

## Примеры использования
```sh
<example.deps.txt ./parse_deps.py | ./restrict_deps.py a | ./deps2dot.py \
    | dot -Tsvg >tmp/example.deps.svg \
    && xdg-open tmp/example.deps.svg

( cd ../../operator-window && ya java dependency-tree ) \
    | ./parse_deps.py | ./restrict_deps.py market/lilucrm \
    | ./remove_nodes.py jmf/utils spring_infrastructure lilu_infrastructure \
    | ./deps2dot.py | dot -Tsvg >tmp/ow.deps.svg \
    && xdg-open tmp/ow.deps.svg
# or same:
./gen_ocrm_deps_graph.sh
```
