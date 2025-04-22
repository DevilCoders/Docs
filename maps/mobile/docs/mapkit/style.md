#Стили карты
В MapKit  можно менять внешний вид отображаемой карты, включая насыщенность и яркость
      цветов, а также их тон.

##Как задать стиль карты
Стиль карты задается с помощью JSON строки следующего вида:
```
[
  {
  "featureType" : "string",
  "stylers" : {
    "hue" : "double",
    "saturation" : "double",
    "lightness" : "double"
    }
  }
]
```
**Внимание:** Обязательные параметры отмечены знаком «*».

|Параметр|Описание|
|---|---|
|featureType|Класс объекта к которому нужно применить стили. Чтобы применить стили ко всем объектам на слое, используйте значение all.|
|stylers|JSON объект, задающий изменения цвета карты в формате HSV.|
|hue|Изменяет цветовой тон объектов на карте. Допустимые значения: от -1 до 1.["hue":0.5](https://jing.yandex-team.ru/files/iudalov/hue05.png) ["hue":-0.5](https://jing.yandex-team.ru/files/iudalov/hue-05.png))|
|saturation|Изменяет насыщенность цветов на карте. Допустимые значения: от -1 до 1.["saturation":1](https://jing.yandex-team.ru/files/iudalov/saturation1.png) ["saturation":-1](https://jing.yandex-team.ru/files/iudalov/saturation-1.png)|
|lightness|Изменяет яркость цветов на карте. Допустимые значения: от -1 до 1.["lightness":0.5](https://jing.yandex-team.ru/files/iudalov/lightness05.png) ["lightness":-0.5](https://jing.yandex-team.ru/files/iudalov/lightness-05.png)|


##Как применить стиль карты
Для применения стилей к карте используйте следующие методы:

* setMapStyle — для изменения стиля основного слоя карты.
* setTrafficStyle — для изменения стиля слоя пробок.

**Android**
```
String style = "[" +
              "  {" +
              "    \"featureType\" : \"all\"," +
              "    \"stylers\" : {" +
              "      \"hue\" : \"1\"," +
              "      \"saturation\" : \"0.3\"," +
              "      \"lightness\" : \"-0.7\"" +
              "    }" +
              "  }" +
              "]";
mapview.getMap().setMapStyle(style);
mapview.getMap().getTrafficLayer().setTrafficStyleWithStyle(style);
```
**iOS**
```
NSString *style = @"["
    "{"
        "\featureType\" : \"all\","
        "\"stylers\" : {"
            "\"hue\" : \"1\","
            "\"saturation\" : \"0.3\","
            "\"lightness\" : \"-0.7\""
        "}"
    "}"
    "]";
[[YMKMap Mapview] setMapStyleWithStyle:style];
[[YMKTrafficLayer Traffic] setTrafficStyleWithStyle:style];
```
