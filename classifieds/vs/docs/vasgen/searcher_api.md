## Vasgen search request 

`grpc`-сервис `vertis.vasgen.grpc.Search/Execute` принимает на вход модель запроса [ExecutionRequest](https://github.com/YandexClassifieds/schema-registry/blob/1dada8f7c6422b0e71884c1451c99167fbc78b23/proto/vertis/vasgen/grpc/search.proto#L25).

### План запроса

`ExecutionRequest.Query.ExecutionPlan.plan_id`

Валидные значения:
 - search
 - count
 - facet - подсчет различных статистик

### Metadata

Описывается с помощью proto класса [`general.search.vasgen.vasgen_model.QueryMetadata`](https://github.com/YandexClassifieds/schema-registry/blob/master/proto/general/search/vasgen_model.proto#L88). 
Полученную типизированные метаданные следует сконвертировать в `sraas.any.Any` и указать в качестве параметра `typed_metadata` 
в [vertis.vasgen.Query](https://github.com/YandexClassifieds/schema-registry/blob/68d2b7ae44f373a2b30bf4f328e1d1f6ebc1a7c2/proto/vertis/vasgen/query.proto#L95).

**Пример в виде json**

```json
{
"metadata": {
      "page_num": "0",
      "page_size": "78",
      "facet_prop_name" : "offer.category.main",
      "facet_limit" : "100",
      "refine_factors" : "f_refine_category:0.9999984:offer.category.all:stroitelstvo-i-remont_h7HBY6;f_refine_category:1.6350776E-6:offer.category.all:listovoy-prokat_vYPldQ"
    },
"typed_metadata" : {
      "value" : "CgIQQBJMChFmX3JlZmluZV9jYXRlZ29yeRXl/38/GhJvZmZlci5jYXRlZ29yeS5hbGwiHmIcc3Ryb2l0ZWxzdHZvLWktcmVtb250X2g3SEJZNhJFChFmX3JlZmluZV9jYXRlZ29yeRXXdNs1GhJvZmZlci5jYXRlZ29yeS5hbGwiF2IVbGlzdG92b3ktcHJva2F0X3ZZUGxkKh8KHW9mZmVyLnByaWNlLnByaWNlX2luX2N1cnJlbmN5",
      "type_id" : {
        "message_name" : "general.search.vasgen.QueryMetadata"
      }
    }
}
```
[**Пример в scalа коде**](https://github.com/YandexClassifieds/vs/blob/master/services/vasgen/searcher/test/src/vasgen/grpc/RequestParamsSpec.scala)

### Query
#### Примеры фильтров

 ##### Целочисленные сравнения в связке `AND`:

```json
{
"filter": {
      "and": [
        {
          "gte": {
            "field": "offer.price.price_in_currency",
            "value": {
              "integer": {
                "sint64": 1000
              }
            },
            "or_equals": false
          }	
        },
        {
          "lte": {
            "field": "offer.price.price_in_currency",
            "value": {
              "integer": {
                "sint64": 10000
              }
            },
            "or_equals": false
          }
        }
      ]
    }
}
``` 

 ##### Гео фильтр
 Ограничения со стороны saas: 
 - в одном запросе может быть только один гео-фильтр
 - только в качестве операнда в верхнеуровневом AND

```json
{
    "filter": {
      "and": [
        {"geo": {
          "radius": {
            "location": {
              "latitude": 55.753215,
              "longitude": 37.622504
            },
            "radius": 5
          }
        }}
        ]
    }
}
```

 ##### `NOT` (ограниченная поддержка)
 
 Использовать только:
 ###### Как верхнеуровневый фильтр: <a name="not"></a>
  - внутренний фильтр - простой терминальный фильтр.
   **Простыми терминальными фильтрами** называются равно, больше, меньше, between, in, гео(за исключением фильтра по географическим координатам)
  - высказывание, составленное из простых терминальных фильтров с помощью `AND` или `OR`. 
  **Упрощений** логических выражений vasgen **не производит**, поэтому, например, выражение, 
  A&(¬B|¬C) = A&¬(B&C), которое, вообще говоря, можно было бы представить в saas как A ~ (B << C), не поддерживается(_soon_)
  - текст - опционально, `NOT` работает с текстом или без него.
```json
{
  "domain": {
    "id": "general"
  },
  "query": {
    "filter": {
      "not": {
        "eq": {
          "field": "seller_id.user_id",
          "value": {
            "string": "4037106905"
          }
        }
      }
    },
    "plan": {
      "plan_id": "general_search"
    },
    "metadata": {}
  }
}
```
###### В качестве одного из операндов в `AND`
 - в этом же `AND` необходим хотя бы один операнд без отрицания: это ограничение saas. 
 - на фильтр под `NOT` распространяются такие же ограничения, как в [верхнеуровневом not](#not).
 - текст - опционально, `NOT` работает с текстом или без него.
```json
{
  "domain": {
    "id": "general"
  },
  "query": {
    "filter": {
      "and": [
        {
          "not": {
            "or": [
              {
                "eq": {
                  "field": "seller_id.user_id",
                  "value": {
                    "string": "4037106905"
                  }
                }
              },
              {
                "and": [
                  {
                    "eq": {
                      "field": "seller_id.user_id",
                      "value": {
                        "string": "4001517379"
                      }
                    }
                  },
                  {
                    "eq": {
                      "field": "offer.price.price_in_currency",
                      "value": {
                        "integer": {
                          "sint64": 0
                        }
                      }
                    }
                  }
                ]
              }
            ]
          }
        },
        {
          "lte": {
            "field": "offer.price.price_in_currency",
            "value": {
              "integer": {
                "sint64": 20000
              }
            },
            "or_equals": false
          }
        }
      ]
    },
    "text": {
      "query": "nintendo switch"
    },
    "plan": {
      "plan_id": "general_search"
    },
    "metadata": {}
  }
}
```


### DSSM

`ExecutionRequest.Query.ranking_vectors`  
Набор векторов, которые ставятся в соответствие запросу.  
Каждый вектор представлен моделью [EmbeddedVector](https://github.com/YandexClassifieds/vs/blob/4255a80b8f3d10ac756297ab3b91490ae5d12e77/lib/schema-registry/proto/vertis/vasgen/common.proto#L58) и имеет помимо самого набора чисел имя и версию.    
Обязательно заполняется поле `product_factor` -- имя фактора, в который запишется результат скалярного перемножения документного вектора на запросный вектор с совпадающими именами.
Имя и версия вектора используются, чтобы найти среди векторов соответствующих документу вектор с таким же именем и версией.  
Если такой вектор найден, то фактору, указанному в `product_factor`, присваивается значение, равное скалярному произведению вектора запроса и вектора документа.  
Фактор зануляется, если:
- среди векторов документа **нет** вектора с таким же именем и версией
- документных эмбеддингов одной версии и типа **несколько** (агрегатные функции над векторами сейчас не поддерживаются)

Если вектора документа и запроса разной размерности, сёрчер вернет ошибку:
```http request
ERROR:
	  Code: Unknown
	  Message: http code: 502, status text: Bad gateway
```

### Refine factor

Рефайн фактор может принимать значения от 0 до 1, значения > 1 будут округлены до 1 ровно.  
Если для одного рефайн-фактора задано несколько условий по которым он сетится, то он примет максимальное из значений, но не более 1.

### Полнотекстовый поиск

Можно указать искомый текст и текст, исключаемый из поиска. 
Поддерживается только поиск **без уточнения зоны поиска**(через поле [```text```](https://github.com/YandexClassifieds/schema-registry/blob/9e1add170ea0521cc5e66cd762e75e9c1dc22d6f/proto/vertis/vasgen/query.proto#L108)) - в таком случае текстовые зонные факторы считаются корректно.

### Аннотации 

Для поиска с учетом аннотации нужно в запросе указать эксперимент _search_in_ann_.