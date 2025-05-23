# Сценарий Яндекс.Такси
Такси хочет посылать нам на вход поток координат контракторов.
У потока следующие свойства:
1. у контрактора 2 уникальных идентификатора, точнее идентификатор контрактора состоит из двух токенов.
2. Каждый из них двигается на каком-то виде транспорта, но Такси пока не передает это явно - вместо этого они дают сервис где эту информацию можно получить.
3. Каждый сигнал который они передают помечен определенный тегом, который называется "источник". Чуть подробнее об этом "источнике" будет позже, но пока что считаем что это просто пользовательский тег который мы никак не интерпретируем.

Что такси потребляет? Такси использует как пуш-модель, когда мы им скармливаем данные по шине, так и poll модель, когда они ходят к нам с запросами. Мы начнем с пуш и в квадратных скобках я указываю те сервисы Такси, которые пользуются этим потоком. Я указываю только наружние по отношению к нам сервисы, т.к. передача данных между нашими сервисами - это вообще внутреннее наше дело и оно "детали реализации".
1. Такси нужен поток данных со теми сырыми координатами всех контракторов, которые помеченны источником Verified. [кандидаты]
2. Такси нужнен поток данных с притянутыми координатами всех контракторов у которых тип транспорта "автомобиль", чья геозона находится в определенном списке стран и где источник "Verified", которые получаются в результате притягивания шины сырых данных (т.е. пункта 1 но только для определенной геозоны). [используется в кандидатах и в chains]. Чуть подробнее тут:
    * Мы сейчас не можем притягивать пеших, поэтому пешие притягивать не надо
    * Так же, мы сейчас не обладаем графом чтобы притягивать часть Европы, Америки и т.п. Поэтому их тоже не надо притягивать.
3. Такси нужна шина со всеми координатами (т.е. без фильтрации по источникам) всех контракторов. Используется в [coords-control]
4. Такси нужна шина в которую пишутся т.н. timelefts для водителей на маршруте - т.е. пакет позиция водителя + время до его точек назначения.

Для poll-модели Такси ходит к нам с такими запросами:
1. Дай нам историю сырых точек для водителя A между датами D1 и D2
2. Дай нам притянутый трек для водителя A между D1 и D2. Важно - нет требования чтобы это был трек исторических приягиваний. Все что требуется - чтобы трек проходил по дорогам. Например можно взять сырой трек, притянуть его и отдать.
3. Дай нам последние N позиций водителя A с источниками [S1, ..., SN]
4. Дай нам шорттрек водителя А сформированный по источникам [S1, ..., SN]
5. Такси хочет получать шорттреки и позиции по запросу для позиций с источником Verified и их притянутых вариантов. Это используется повсеместно.
6. Такси хочет получать позиции для определенного набора источников запросом с ретраями на случай отсутствия. Это используется например в логине где координата очень нужна.
7. Такси также хочет получать притянутые позиции Verified с альтернативами - это используется в ML

## Настройки входного потока
Сейчас этот сценарий реализован такой конфигурацией каналов:

1. Весь пакет отправляется в канал channel:yagr:signal_v2 - это поток данных из пункта 3 сценария.
   INSERT INTO 'channel:yagr:signal_v2' SELECT *
2. Распределяем Verified сигналы в зависимости от типа транспорта и от региона
   Эти 4 канала образуют поток данных из пункта 1 сценария.
   INSERT INTO 'channel:yagr:pedestrian_positions' SELECT * WHERE transport_type != 'car' AND region not in WorldRegionsSet
   INSERT INTO 'channel:yagr:positions' SELECT * WHERE transport_type = 'car' AND region not in WorldRegionSet
   INSERT INTO 'channel:yagr:world:pedestrian_positions' SELECT * WHERE transport_type != 'car' AND region in WorldRegionsSet
   INSERT INTO 'channel:yagr:world:positions' SELECT * WHERE transport_type = 'car' AND region in WorldRegionSet

Вот так выглядит конфигурация Ягра

{% code './taxi.yaml' lang='yaml' jsonpath='$.taxi.input' %}

## Настройки притягивателя
Yaga подписанна на канал channel:yagr:positions. Она считывает оттуда точки, притягивает их и публикует в канал channel:yaga:edge_positions.

{% code './taxi.yaml' lang='yaml' jsonpath='$.taxi.yaga' %}

## Настройки хранения
4. Сервис internal-trackstory подписан на все потоки и записывает данные в редис. Он отвечает на все poll-запросы Такси.

TODO: Описать настройки

## Пример потока данных

### Happy path

Пусть на вход приходят такая позиция

```yaml
timestamp: 1649970983056
source: "Verified"
transport_type: "car"
region: "moscow"
positions:
  - time_shift: 0
    positions:
      - position: [52.569089, 39.60258]
        accuracy: 5
        speed: 16.6
        direction: 125
```

Она подходит под два фильтра и отправляется в
1. канал raw_driver_positions
2. во внутренний поток для архивации (деталь реализации- логброкер , завтра может быть и не логброкер)
3. канал signal_v2_positions

На этот канал есть обработчки в yaga. Он считывает эту позицию и  согласно своим
настройкам отправляет в канал "adjusted_driver_positions" притягивание и
предсказание. Эта позиция записанна во внутреннем формате, но по сути
эквивалентна такой структуре

```yaml
timestamp: 1649970983056
source: "Adjusted"
transport_type: "car"
region: "moscow"
positions:
  - time_shift: 0
    positions:
      - position: [52.569091, 39.60256]
        accuracy: 5
        speed: 16.6
        direction: 115
  - time_shift: 10
    positions:
      - position: [52.569093, 39.60252]
        accuracy: 5
        speed: 16.6
        direction: 105
```


На эту позицию подписанны два сервиса: driver-route-watcher, который пока не
входит в описываемую часть системы и сервис хранения позиций.

Сервис internal-trackstory считывает позицию и хранит ее в редисе заданное
время.

Сервис internal-trackstory настроен таким образом, что он хранить 'Verified'
источники несколько часов, 'Adjusted' - 15 минут, а все остальные - последние 5
позиций.

### Вторичный источник

Пусть на вход приходит вот такая позиция
```
timestamp: 1649970983056
source: "AndroidGps"
transport_type: "car"
region: "moscow"
positions:
  - time_shift: 0
    positions:
      - position: [52.569089, 39.60258]
        accuracy: 5
        speed: 16.6
        direction: 125
```

Она подходит только под один фильтр и отправляется в канал signal_v2_positions

