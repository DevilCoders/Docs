# Адреса продажи

В качестве адреса продажи во внутреннем API используется общая 
[модель](https://github.com/YandexClassifieds/schema-registry/blob/master/proto/general/common/address_model.proto).

## Описание полей модели
- `geopoint` - координаты точки продажи. 
Существует всегда, даже если пользователь сервиса хочет указать в качестве адреса целый город

- `metro_station` - станция метро. Например, станция "Маяковская" в Москве.
Дополнительно вместе со станцией указываются номера линий, на которой находится станция.
Это обусловлено возможностью указать конкретную линию для станций, 
находящихся сразу на нескольких линиях (например, "Киевская" в Москве). 
Соответствует топониму `MetroStation`

- `district` - район города. Например, "Тверской район" в Москве.
Соответствует топониму `District`

- `region` - регион (село, город, субъект федерации).
Соответствует топониму `Region`

- `address` - любой объект, не попадающий под указанную выше классификацию 
(например, улица и номер дома, либо просто название улицы). 
Например, таким адресом является "Рыбный переулок, 3", "Красная площадь" или "Невский проспект".
Соответствует топониму `Address`

## Сценарии создания адреса

### Анкета пользователя
- строковый адрес (пользовательский ввод):

  Используем геосаджест из `globe`, получаем `Toponym`. 
  Сохраняем `geopoint` и одно поле из `{metro_station, district, region, address}`
  
- строковый адрес + координаты (из персонализации):

  Сохраняем `geopoint` + `address`.
  TODO: Возможно, стоит использовать геосаджест

### Форма добавления
- координаты:

  Используем обратное геокодирование из `globe`. 
  Сохраняем `geopoint` и `address`
  
- строковый адрес (пользовательский ввод):

  Используем геосаджест из `globe`, получаем `Toponym`. 
  Сохраняем `geopoint` и одно поле из `{metro_station, district, region, address}`


### Фиды
- координаты:

  Используем обратное геокодирование из `globe`. 
  Сохраняем `geopoint` и `address`
  
- строковый адрес:

  Используем прямое геокодирование в `globe`, берем первый результат, получаем `Toponym`.
  Сохраняем `geopoint` и одно поле из `{metro_station, district, region, address}`
  
---

TODO: возможно в сценариях с обратным геокодированием тоже имеет смысл различать топонимы

## Обязательные поля при хранении
При сохранении объявления в базу `gost`'а адрес продажи обязан содержать:
 
- Координаты
- Информацию о регионе (поле `region`).
Данное поле обогащается из других данных, если пользователь не указывает это поле.
- Если регионом не является маленький город, 
то должно содержатся любое поле из множества: `{metro_station, district, address}`
(CLASSBACK-220)

При сохранении в анкету пользователя адрес обязан содержать:
- Координаты
- Одно любое заполненное поле из оставшихся

## Обогащение адреса

При ручном создании объявления адрес обогащается перед публикацией.

TODO: когда обогащается адрес в фидах?

Все поля обогащаются исходя из указанной географической позиции.
(При обогащении станциями метро берется ближайшая станция в определенном радиусе. 
Возможно, имеет смысл обогащать множеством станций метро).

Множество обогащаемых полей определяется по заполненной компоненте адреса по следующим правилам:

- `address` -> {`metro_station`, `district`, `region`}
- `metro_station` -> {`district`, `region`}
- `district` -> {`region`}
- `region` -> Ø

## Поиск

Два типа поиска:

- Поиск по id региона, id районов и id станций метро
- Поиск по координатам и радиусу

### Индексация в поиске (TODO)

Сервис `search` извлекает из адресов объявления 4 множества:

- множество идентификаторов регионов
- множество идентификаторов станций метро
- множество идентификаторов районов
- множество точек на карте (`geopoint`)

По множеству идентификаторов регионов с помощью сервиса `globe` (TODO: написать API) 
получает все идентификаторы родительских регионов (не обязательно непосредственных родителей).

Идентификаторы станций метро, районов и регионов (вместе с родительскими) 
записываются в отдельные поля поискового документа.

Множество точек на карте записывается в поле со специальным типом.

## Проблемы:

### Удаление географических объектов

Географические объекты могут быть удалены.
В таком случае какую-то информацию об объекте получить будет невозможно.

В данный момент для решения этой проблемы названия всех объектов и цвета линий у станций метро
хранятся прямо в модели, а не получаются по `id` из `globe`.

В дальнейшем предполагается не хранить эти данные в модели, а при отсутствии объекта в `globe` 
восстанавливать информацию через обратное геокодирование. 
Для уменьшения нагрузки на геокодер понадобится либо фоновое преобразование таких адресов, 
либо "ленивое" изменение адреса в базе при первом запросе.

### Передача названий объектов с фронтенда
Это порождает уязвимости в сервисе: 
пользователь может "вручную" обратиться к API сервиса и, например, 
передать произвольные строки в название объектов или произвольные цвета станций.

Возможные решения для информации о станции метро, районе или регионе:

1. Информацию можно получать при создании адреса по `id` объектов, а не получать с фронтенда

2. Вообще не хранить дополнительную информацию. (См. пункт "Удаление географических объектов")


Возможные решения для точного адреса (`address`):

1. Обратное геокодирование 
(в таком случае может изменится корректное представления адреса, который пользователь выбрал из саджеста)

2. Прямое геокодирование строки с адресом и сравнение полученной координаты с переданной в `geopoint`
