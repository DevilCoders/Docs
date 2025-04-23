# node-yson

Node.js биндинги к [libyson](https://github.yandex-team.ru/yson/libyson) с помощью [node-addon-api](https://github.com/nodejs/node-addon-api)

### Установка

```
apt-get install libyson-dev
```
затем:
```
npm install --registry=https://npm.yandex-team.ru/ node-yson
```

Доступно только для Linux, чтобы поддержать разработку на MacOs нужно расширить файл ```binding.gyp```.

### Типы данных
```
YSON {
    type Scalar = number | boolean | Buffer | undefined;
    type Map = Record<string, Node>;
    type Attributes = Map;
    type List = Array<Node>;

    type Value = Scalar | Map | List;
    type ValueWithAttributes = (Number | Boolean | Buffer | {} | Map | List) & {attributes?: Attributes};

    type Node = Value | ValueWithAttributes;
}
```

### Доступные методы

#### YSON.parse
Разбирает YSON данные.
##### Параметры
```buffer``` - ```Buffer | string```. Разбираемый буфер YSON. Смотрите документацию по объекту [YSON](https://yt.yandex-team.ru/docs/description/common/yson) для описания синтаксиса YSON.

```mode``` - ```"YSON_STREAM_TYPE_NODE" | "YSON_STREAM_TYPE_LIST_FRAGMENT" | "YSON_STREAM_TYPE_MAP_FRAGMENT"```. [Формат данных](https://wiki.yandex-team.ru/yt/internal/yson/) YSON.

##### Возвращаемое значение
Возвращает объект: ```YSON.Node | YSON.List```.
Примечание: При отсутствии атрибутов, порождает значение ```YSON.Node=YSON.Value```, иначе - ```YSON.Node=YSON.ValueWithAttributes```,при этом в ```YSON.ValueWithAttributes``` примитивы будут использоваться как объекты.


#### YSON.stringify
??? - Если возникнет необходимость. Welcome)
