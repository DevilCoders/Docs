# Генерация схемы

Для генерирования схемы для своего сервиса, надо передать объект сообщения в функцию генерации `def make_config_module(message)`,
которая запишет модуль со схемой в стандартный поток вывода.

# Нормализация

Процесс нормализации убирает все лишние поля из объекта, основываясь на его схеме.

Для нормализации схемы используется функция `def normalize_by_schema(config, schema=None)`. 
Она принимает схему в словаря и config, возвращает нормализованный словарь конфигурации. 
Функция нормализации так-же отслеживает ошибки типов или некоторые противоречия, например:
- если поле имеет тип string, а мы хотим передать туда int
- стоит oneof, а мы выставили два поля
- repeated, а мы передаем одиночное значение

# Пример генерации

Для генератора схемы надо будет описать цель для ymake.

ya.make:
```
SET(CONFIG_PROTO_LIB ads/bsyeti/raven/proto)
SET(CONFIG_PROTO_FILE config.proto)
SET(CONFIG_PROTO_CLASS TConfig)
INCLUDE(${ARCADIA_ROOT}/ads/bsyeti/samogon/plugin_lib/config_normalizer/generator/ya.inc)
```

В итоговой сборке проекта, нужно будет подключить генератор с помощью RUN_PROGRAM и сохранить вывод в файл.
пример:
```
RUN_PROGRAM(
    ads/bsyeti/samogon/raven/config/generate STDOUT_NOAUTO ${ARCADIA_BUILD_ROOT}/raven_config.py
)

SET(EXTRA_FILE_PATH ${ARCADIA_BUILD_ROOT})
SET(EXTRA_FILE raven_config.py)

INCLUDE(${ARCADIA_ROOT}/ads/bsyeti/samogon/plugin_lib/extra.inc)
```

# Формат ProtoSchema

ProtoSchema - описание устройства Protocol Buffer через json. 
Используется для проверки JSON-объектов которые описывают Protobuf, 
в условиях когда вы не можете подключить Protobuf-библиотеку :). 
Вся схема, это JSON-объект с описанием сообщения по следующим правилам:

Каждое сообщение состоит из словаря пар (<имя_поля>: <описание_поля>):

Каждое описание поля имеет тип поля (type), в зависимости от типа, могут быть доп. поля.

Если поле являеется членом oneof, то оно также будет содержать:
- oneof: название oneof

Если поле является обязательным, тогда оно также будет содержать:
- required: 1

Если поле имеет тип enum, то оно содержит:
- enum: допустимые значения для поля 

Если поле имеет тип object, тогда оно содержит
- object: схема объекта

Если поле имеет тип list, тогда оно содержит
- item: схема одного элемента в списке

# Примеры описания полей

```proto
message TAllMessage {
    required string StrReq = 1;
    optional string StrOpt = 2;

    message TMapVal {
        optional string MapStrOpt1 = 1;
        optional string MapStrOpt2 = 2;
    }
    map<string, TMapVal> MapStrStr = 3;

    enum ETypo {
        TYPO_0 = 0;
        TYPO_2 = 2;
        TYPO_3 = 3;
        TYPO_5 = 5;
    };
    required ETypo Typo = 4;

    message TOneVal {
        repeated string StrArr = 1;
        required uint64 Size = 2;
    };

    oneof OneOne {
        TOneVal OneVal = 5;
        string OneArr = 6;
        int32 OneNum = 7;
    }
};
```

Схема:
```json
{
  "type": "object",
  "object": {,
      "StrReq": {
        "required": true,
        "type": "string"
      },
      "StrOpt": { "type": "string" },
      "MapStrStr": {
        "type": "object",
        "object": {
            "key": { "type": "string" },
            "value": {
                "type": "object",
                "object": {
                    "MapStrOpt1": { "type": "string" },
                    "MapStrOpt2": { "type": "string" }
                }
            }
        }
      },
      "Typo": {
        "type": "enum",
        "enum": ["TYPO_0", "TYPO_2", "TYPO_3", "TYPO_5", 0, 2, 3, 5],
        "required": true
      },
      "OneVal": {
        "oneof": "OneOne",
        "type": "object",
        "object": {
            "StrArr": {"type": "list", "item": {"type":  "str"}},
            "Size": {
                "type": "uint64", 
                "required": true
            }
        }
      },
      "OneArr": {
        "oneof": "OneOne",
        "type": "string"
      },
      "OneNum": {
        "oneof": "OneOne",
        "type": "int32"
      }
  }
}
```
