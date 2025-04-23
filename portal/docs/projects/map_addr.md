# MapAddr

Go-микросервис, призванный заменить устаревший C++-блок, который выполняет запросы в Геопоиск для получения компонентов адреса по координатам пользователя:

* подготавливает запрос в Геопоиск
* разбирает полученный бинарный ответ в формате Protobuf и отдаёт наружу форматированную JSON-ку

Вызывается как внешний сервис (subreq) в Morda Perl в ручках `/gpsave` и `/portal/api/yabrowser/2`.

## Как пользоваться {#api}

* `lat, lon` – обязательные аргументы, задающие координаты пользователя как вещественные числа
* `lang` – опциальный аргумент, определяющий язык ответа. Задаётся как код по формату ISO 639-1, например:
  - `ru` – русский язык
  - `en` – английский язык 
  - `uk` – украинский язык
  - `kk` – казахский язык
  - `be` – белорусский язык 

    Если аргумент не указан или используется невалидное или пустое значение, то по умолчанию используется русский язык.

Примеры:

* [https://l7test.yandex.ru/geohelper/map_addr?lon=37.518813&lat=55.929433](https://l7test.yandex.ru/geohelper/map_addr?lon=37.518813&lat=55.929433)
```(json)
{
  "components": [
    {
      "kind": "country",
      "name": "Россия"
    },
    {
      "kind": "province",
      "name": "Центральный федеральный округ"
    },
    {
      "kind": "province",
      "name": "Московская область"
    },
    {
      "kind": "area",
      "name": "городской округ Долгопрудный"
    },
    {
      "kind": "locality",
      "name": "Долгопрудный"
    },
    {
      "kind": "street",
      "name": "Институтский переулок"
    },
    {
      "kind": "house",
      "name": "9с3"
    }
  ],
  "formatted": "Россия, Московская область, Долгопрудный, Институтский переулок, 9с3",
  "internal": {
    "geoid": 214,
    "house_count": 0,
    "point": {
      "lon": 37.5188115777149,
      "lat": 55.929434395956996
    },
    "matched_component": [
      {
        "kind": 7
      }
    ],
    "seoname": "institutskiy_pereulok_9s3"
  },
  "show": 1,
  "type": "MapAddr_formatted"
}
```

* [https://l7test.yandex.ru/geohelper/map_addr?lat=55.776853&lon=37.656959&lang=ru](https://l7test.yandex.ru/geohelper/map_addr?lat=55.776853&lon=37.656959&lang=ru)

```(json)
{
  "components": [
    {
      "kind": "country",
      "name": "Россия"
    },
    {
      "kind": "province",
      "name": "Центральный федеральный округ"
    },
    {
      "kind": "province",
      "name": "Москва"
    },
    {
      "kind": "locality",
      "name": "Москва"
    },
    {
      "kind": "street",
      "name": "Комсомольская площадь"
    },
    {
      "kind": "house",
      "name": "5"
    }
  ],
  "formatted": "Россия, Москва, Комсомольская площадь, 5",
  "internal": {
    "geoid": 213,
    "house_count": 0,
    "point": {
      "lon": 37.656963485259645,
      "lat": 55.77685138958492
    },
    "matched_component": [
      {
        "kind": 7
      }
    ],
    "seoname": "komsomolskaya_ploshchad_5"
  },
  "type": "MapAddr_formatted",
  "show": 1
}
```

* [https://l7test.yandex.ru/geohelper/map_addr?lon=37.587093&lat=55.733974&lang=en](https://l7test.yandex.ru/geohelper/map_addr?lon=37.587093&lat=55.733974&lang=en)

```(json)
{
  "components": [
    {
      "kind": "country",
      "name": "Russia"
    },
    {
      "kind": "province",
      "name": "Tsentralny federalny okrug"
    },
    {
      "kind": "province",
      "name": "Moscow"
    },
    {
      "kind": "locality",
      "name": "Moscow"
    },
    {
      "kind": "street",
      "name": "Lva Tolstogo Street"
    },
    {
      "kind": "house",
      "name": "16"
    }
  ],
  "formatted": "Russia, Moscow, Lva Tolstogo Street, 16",
  "internal": {
    "geoid": 213,
    "house_count": 0,
    "point": {
      "lon": 37.587092522460836,
      "lat": 55.73397404565889
    },
    "matched_component": [
      {
        "kind": 7
      }
    ],
    "seoname": "ulitsa_lva_tolstogo_16"
  },
  "type": "MapAddr_formatted",
  "show": 1
}
```
  
* [https://l7test.yandex.ru/geohelper/map_addr?lat=50.447229&lon=30.523118&lang=uk](https://l7test.yandex.ru/geohelper/map_addr?lat=50.447229&lon=30.523118&lang=uk)

```(json)
{
  "components": [
    {
      "kind": "country",
      "name": "Україна"
    },
    {
      "kind": "province",
      "name": "Київ"
    },
    {
      "kind": "locality",
      "name": "Київ"
    },
    {
      "kind": "street",
      "name": "вулиця Хрещатик"
    },
    {
      "kind": "house",
      "name": "19"
    }
  ],
  "formatted": "Україна, Київ, вулиця Хрещатик, 19",
  "internal": {
    "geoid": 143,
    "house_count": 0,
    "point": {
      "lon": 30.52311842056424,
      "lat": 50.44722904851273
    },
    "matched_component": [
      {
        "kind": 7
      }
    ],
    "seoname": "vulytsia_khreshchatyk_19"
  },
  "type": "MapAddr_formatted",
  "show": 1
}
```


## Деплой {#deploy}
Окружение     | URL
----------------|----------------------------------------------------------------
Тестинг         | `https://l7test.yandex.ru/geohelper/map_addr`
Продакшн        | `http://geohelper-internal.yandex.net:8888/map_addr`<br>_(доступен только с dev-стендов и продовых хостов Morda Perl)_
Хамстер         | `http://avocado-dev.yandex.net/map_addr`

## Где искать мониторинги и панели {#monitoring}

* Алерты от Аппхоста вида `portal.apphost.avocado.apphost.map_addr*`, сгенерированные шаблоном: [https://yasm.yandex-team.ru/template/alert/portal.apphost.avocado](https://yasm.yandex-team.ru/template/alert/portal.apphost.avocado)
* Алерты на потребление ресурсов бэкендом вида `portal.mapaddr.infra.*`: [https://yasm.yandex-team.ru/template/alert/portal.mapaddr/](https://yasm.yandex-team.ru/template/alert/portal.mapaddr/)
* Панель сигналов на вершины графа: [https://yasm.yandex-team.ru/template/panel/apphost_template/graph=map_addr/](https://yasm.yandex-team.ru/template/panel/apphost_template/graph=map_addr/)
* Панель Error Booster на граф `map_addr`: [https://nda.ya.ru/t/qzgyDmow4sdzSY](https://nda.ya.ru/t/qzgyDmow4sdzSY)
* Панель метрик микросервиса: [https://nda.ya.ru/t/psONJPar4si2d8](https://nda.ya.ru/t/psONJPar4si2d8)
* Статистика кодов и времён ответа ручки `/gpsave`, в которой используется MapAddr: [https://yasm.yandex-team.ru/template/panel/morda-handlerstat-common-2/prj=portal-morda;filter=gpsave/](https://yasm.yandex-team.ru/template/panel/morda-handlerstat-common-2/prj=portal-morda;filter=gpsave/)
* RPS и время ответа старого бэкенда `map_addr` в C++-блоке (через локальный Аппхост): [https://yasm.yandex-team.ru/template/panel/morda_subreqname/alias=map_addr;mode=full/](https://yasm.yandex-team.ru/template/panel/morda_subreqname/alias=map_addr;mode=full/)
* RPS и время ответа нового бэкенда `avocado_map_addr` через микросервис [https://yasm.yandex-team.ru/template/panel/morda_subreqname/alias=avocado_map_addr;mode=full/](https://yasm.yandex-team.ru/template/panel/morda_subreqname/alias=avocado_map_addr;mode=full/)
