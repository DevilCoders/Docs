## Управление ограничениями multiselect требований через flavor-ы

_Glossary_: требования == пожелания

В рамках объединения Детских кресел было создано multiselect требование [childchair_v2](https://tariff-editor.taxi.yandex-team.ru/requirements/edit/childchair_v2)
которое может иметь разные параметры max_weight/weight/max_count (а также некоторые другие) в разных зонах и категориях
[RFC про childchair_v2](https://github.yandex-team.ru/taxi/rfc/blob/childchair_v2/requirements/childchair_v2.md)

Актуальные параметры пока берем из эксперимента [requirement_overrides_childchair_v2](https://tariff-editor.taxi.yandex-team.ru/experiments3/experiments/show/requirement_overrides_childchair_v2/current?name=requirement_override&enabled=all&active=all)

### Flavors
Максимально гибкое решение -- позволять для каждой категории и зоны указать весь набор параметров -- не подходит, тк это будет запутанно и будет приводить к человеческим ошибкам. На практике более удобно оперировать набором готовых flavor-ов или
комбинаций параметров.

Рассматриваемое решение даст возможность:
1. Не накликивать для каждой зоны и категории все 7 чисел, а использовать готовые комбинации
2. Отключать показ некоторых опций, не создавая отдельного требования (помимо того что это костыльно оно ещё и не ложится на новый флоу Детского)

Сейчас существует 3 основные комбинации max_weight/weight/max_count, соответствующих "старым" Детским требованиям
childchair_for_child_tariff (1 infant, 1 chair, 2 booster)
double_childchair_moscow (2 infant, 2 chair, 2 booster)
childchair_moscow (1 infant, 1 chair, 1 booster)

_формула доступности опций_:
  опцию можно добавить `count` раз, если:
  `sum(opt.weight for opt in selected_opts) <= max_weight && count <= opt.max_count`

#### Дополнительные параметры flavor-а
* tariff_specific - влияет на логику показа баббла недоступного пожелания
  Для Детских кресел правило такое: в Детском тарифе tariff_specific: true, в других false
  Поэтому, чтобы для каждого flavor-а не создавать 2 версии с разным tariff_specific,
  лучше сделать его флагом пожелания в настройках зоны (не задавать во flavor-е)
  (см. подробности ниже)
 
* options_drop_sequence - последовательность сброса недоступных опций при переключении между категориями
  Например: `["booster", "chair", "infant"]`

### Flavor и отсутствующие опции
В ближайшем будущем собираемся запускать новые опции для существующих Детских пожеланий:
свое кресло, люлька до 1 года (bassinet). Хочется управлять этим через flavor-ы, не создавая отдельных пожеланий.
Уже сейчас есть зоны и категории, в которых не видны некоторые опции. Например, сейчас в Эстонии нет опции Бустер,
для этого там используется требование childchair_kazan.
__Предлагается__:

1. Задать в пожелании childchair_v2 все параметры для новой опции: name, value, weight, max_count

   _Пример_: для люльки до 1 года
   `name = bassinet, value = 0, weight = 2, max_count = 1` -- кстати уже кем-то используется в тестинге

2. Отсутствие в существующих флейворах ограничений для новой опции означает что по умолчанию она не видна.
3. Создать flavor и добавить в options ограничения для новой опции, а также обновить options_drop_sequence
4. В настройках зоны выбрать новый флейвор

### Админка пожеланий и flavors

![image](static/flavor_edit.png)

В API появляются поля `supports_flavors` и `flavors`
Для `supports_flavors: true` пожеланий:
1. виден список "Flavors" существующих (в виде списка по отсортированным ключам `flavors`)
2. По выбору списке открывается форма редактирования флейвора (см. ниже)
3. отображается кнопка "Add flavor" открывающая форму редактирования нового флейвора.

Интерфейс для создания-редактирования флейвора:
1. Имя флейвора
2. Максимальный вес (max_weight) -- по умолчанию `max_weight` пожелания
3. Опции -- для нового по умолчанию видны все, значения weight/max_count по умолчанию такие же как в `select.options[]`
   Можно удалить опцию из флейвора (будет означать что она не будет видна в пожелании
4. Порядок сброса опций (options_drop_sequence) -- редко будет отличаться от дефолтного
   - Дефолт: все опции флейвора в порядке возрастания `options[].value` с возможностью перестановки.
   - Интерфейс создания списка из ограниченного набора по `options[].name`
   - Каждая опция должна быть включена 1 раз.
5. Кнопка "Done/готово" (либо по ESC) скрывающая форму

При наличии изменений становится доступной кнопка "Сохранить"

### API
В ручке создания и редактирования пожелания в админке добавляем опциональные поля:
```
supports_flavors: true,   //
flavors: {
  "1_1_2": {    // Удобная конвенция для имени -- max_count-ы всех опций
      "options": {
        "chair": {
          "weight": 2,
          "max_count": 1
        },
        "infant": {
          "weight": 2,
          "max_count": 1
        },
        "booster": {
          "weight": 1,
          "max_count": 2
        }
      },
      "max_weight": 3,
      "options_drop_sequence": [
        "booster",
        "chair",
        "infant"
      ]
    },
    ... // другие флейворы
}
```

Схема флейвора:
```
  Flavor:
    type: object
    additionalProperties: false
    required:
      - max_weight
      - options_drop_sequence
      - options
    properties:
      max_weight:
        type: integer
      options_drop_sequence:
        type: array
        items:
          type: string
      options:
        type: object
        additionalProperties:
          $ref: '#/definitions/OptionOverride'

  OptionOverride:
    type: object
    additionalProperties: false
    required:
      - max_count
      - weight
    properties:
      max_count:
        type: integer
      weight:
        type: integer
```

## Настройки зоны и пожелания

![image](static/tariff_settings_reqs.png)

#### is_glued & is_persistent как флаги
Сейчас полный список пожеланий задается в client_requirements, и для определения различных флагов пожелание надо добавить
в доп списки: glued_requirements и persistent_reqs
Предлагается изменить интерфейс и использовать здесь флаги: is_glued, is_persistent
API при этом не меняется: помеченные флагами пожелания добавляются соответственно в glued_requirements и persistent_reqs

#### tariff_specific в настройках зоны
Сейчас в 99% случаев tariff_specific совпадает с заданным в админке требований, но есть 2 способа кастомизировать этот флаг для зоны и категории:
1. (устаревший) конфиг [TARIFF_SPECIFIC_OVERRIDES](https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/TARIFF_SPECIFIC_OVERRIDES)
2. Эксп [requirement_overrides_childchair_v2](https://tariff-editor.taxi.yandex-team.ru/experiments3/experiments/show/requirement_overrides_childchair_v2/current)

Чтобы избавиться от обоих надо добавить tariff_specific в настройки зоны, для этого предлагается:
1. Завести _optional_ поле `categories[].tariff_specific_overrides` в API админки и dbtaxi.tariff_settings вида
```
{
  "childchair_v2": false,
  "door_to_door": true
}
```
1. Добавить к описанным выше флаг is_tariff_specific, его значение по умолчанию должно совпадать с `tariff_specific` флагом админки пожеланий, а при наличии пожелания в `tariff_specific_overrides` -- значение оттуда.
2. Для получения значения по умолчанию сделать ручку админки пожеланий `GET /v2/requirements` которая отдает не список названий требований как старая а объекты вида
```
{
  "name": "childchair_v2",
  "is_tariff_specific": true
}
``` 
3. При изменении флага пользователем менять `tariff_specific_overrides`


### Настройки зоны и flavor-ы
Похожим образом добавляем флейворы:
1. В API `GET /api/tariff_settings/{zone_name}/`, `POST /api/set_tariff_settings/{zone_name}/` из py2 и dbtaxi.tariff_settings добавляем опциональный `categories[].requirement_flavor` вида:
```
{
  "childchair_v2": "1_1_1"
}
```
2. Добавляем в `GET /v2/requirements` флаг `supports_flavors` и список `flavors`
```
{
  "name": "childchair_v2",
  "is_tariff_specific": true,
  "supports_flavors": true,
  "flavors": ["1_1", "1_1_1", "1_1_2", "2_2_2"],
}
```
3. По его наличию при добавлении пожелания в client_requirements или редактировании появляется возможность выбрать flavor (без него пожелание с `supports_flavors` добавить нельзя), выбор сохраняется в `/categories[].requirement_flavor`

