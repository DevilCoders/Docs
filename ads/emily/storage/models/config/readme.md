# Валидационный конфиг

## Current config version: __`2.0.0`__

Валидационный конфиг - json файл, в котором описаны продовые модели, валидируемые индексером. Конфиг собирается из нескольких конфигов, лежащих по пути __./data/*__. Среди них:

* [merge_rule.json](./data/merge_rule.json) - перечень правил, по которым нужно мержить конфиги
* [validators.json](./data/validators.json) - валидаторы моделей

Конфиги с моделями:
- [catboosts.json](./data/catboosts.json) - конфиг с катбустами
- [tsars.json](./data/tsars.json) - конфиг с царями
- [linear_models.json](./data/linear_models.json) - конфиг с линейными моделями

## Правила склеивания конфигов
Правила описаны в файле `merge_rule.json`. В поле `meta` указано поле `format_version` - версия формата конфига. Затем в поле `configs` лежат конфиги, которые необходимо смержить. Правило состоит из полей:
- `key` - название конфига. 
- `type` - тип конфига. Поддерживаемые типы:
- - `models` - конфиг с моделями
- - `validators` - конфиг с валидаторами
- `defaults` - дефолтные значения для полей моделей/валидаторов. Например, для катбустов дефолтом проставляются поля:
- - `deploy_bs: true` - отдавать модель движку
- - `validator: catboost` - дефолтный валидатор катбустов
- - `tags: mx` - тег для определения типа модели


## Валидаторы
Валидаторы - это бинари, которые сторадж загружает и применяет на папке с моделью. В случае успешной работы валидатора модель переливается в продовое окружение. Доступные валидаторы:

- `catboost` - валидатор катбустов. Проверяет, что модель имеет части `model`, `meta`, `dump`. Также проверяет валидность файла `meta/meta.json` и валидность катбуста `model/model.bin`. Если у модели нет дампа `dump`, то нужно указать это в поле `validator_options` (Примеры есть в конфиге [catboosts.json](./data/catboosts.json)).
- `dummy` - Простой валидатор. При его использовании рекомендуется переопределять опцию `dump_keys` и перечислять все части модели.

Если ни один из валидаторов не устраивает, можно написать свой валидатор или оформить [фич реквест](https://st.yandex-team.ru/createTicket?queue=LOGOSWEB&_form=46955) команде стораджа

## Модели

Каждая модель определяется следующими основными полями:

- Имя модели - обяательное поле `key`.
- Версия/версии модели. Версия имеет вид `"DD-MM-YYYYThh:mm:ss"` и определяется одним из полей:
    * `start_from_version` - Будут валидироваться все модели, начиная с указанной версии. Добавлять эту опцию следует только регулярным моделям.
    * `version` - версия модели.
- Валидатор модели - ключ одного из валидаторов из поля `validators`.
- Теги для модели - список `tags`.
- Список овнеров `owners`.
- Для добавления катбуста в движок нужно указать поле `deploy_bs` со значением `true`.
- Конфигурация алертов для регулярных моделей - поле `life`. Содержит словарь из опциональных полей `update_time` -- максимальное время с момента публикации последнего valid ресурса и `version_lag` -- максимальная разница между текущей датой и версией модели.

## Пример конфига

```json
{
    "meta": {
        "format_version": "2.0.0"
    },
    "validators": {
        "catboost": {
            "type": "stable",
            "resource_type": "ML_STORAGE_CATBOOST_VALIDATOR_BINARY",
            "options": {
                "corruption_check": true,
                "dump_keys": [
                    "model",
                    "meta",
                    "dump"
                ]
            }
        },
        "dummy": {
            "type": "stable",
            "resource_type": "ML_STORAGE_DUMMY_VALIDATOR_BINARY",
            "options": {
                "dump_keys": [
                    "meta"
                ]
            }
        }
    },
    "models": [
        {
            "key": "1__home__ads__robot-online-pytorch__new_production_online_learning_tsar_ffn_2__tsar_processed_model",
            "start_from_version": "2021-06-30T00:00:00",
            "validator": "dummy",
            "validator_options": {
                "dump_keys": [
                    "BannerNamespaces",
                    "PageNamespaces",
                    "UserNamespaces_3",
                    "meta",
                    "tensor_model"
                ]
            },
            "life": {
                "update_time": "5h",
                "version_lag": "1d"
            },
            "owners": [
                "alxmopo3ov",
                "ya-philya"
            ],
            "tags": [
                "tsar",
                "pytorch_tsar_1"
            ]
        },
        {
            "key": "__home_ads_robot-online-pytorch_bc_rsya_torchv2_hitsplit",
            "start_from_version": "2021-06-15T21:00:00",
            "validator": "dummy",
            "validator_options": {
                "dump_keys": [
                    "banner",
                    "conv_tensor",
                    "meta",
                    "user_page",
                    "user_profile",
                    "user_top"
                ]
            },
            "life": {
                "update_time": "11h",
                "version_lag": "2d12h"
            },
            "owners": [
                "blv1mk"
            ],
            "tags": [
                "tsar",
                "bc_rsya_torch_tsar"
            ]
        },
        {
            "key": "CPM_F7_catboost_sample_ratio_19",
            "version": "2019-11-16T00:00:00",
            "validator": "catboost",
            "tags": [
                "mx"
            ],
            "deploy_bs": true
        },
        {
            "key": "bc_rsya_catboost_regular_llmax_threshold01_sclick_stage2",
            "start_from_version": "2021-09-08T00:00:00",
            "validator": "catboost",
            "validator_options": {
                "dump_keys": [
                    "model",
                    "meta"
                ],
                "check_metrics": {
                    "emily_metrics": [
                        {
                            "key": "Q_SOFTMAX_GAIN",
                            "min_value_learn": 2.5
                        }
                    ]
                }
            },
            "life": {
                "update_time": "2d12h"
            },
            "tags": [
                "mx"
            ],
            "owners": [
                "aschern"
            ],
            "deploy_bs": true
        }
    ]
}
```



## Changelog

- __2.0.0__ Конфиг разделён на несколько конфигов
- __1.1.0__ Из конфига убраны MXID, теперь они будут выдаваться автоматически при валидации.
- __1.0.0__ Рефакторинг конфига.
    * Добавилось глобальное `validators`, в котором лежит словарь с дефолтными валидаторами (`catboost` и `dummy`). Теперь в каждой модели нужно указать в поле `validator` только ключ из этого словаря, в обработке конфига валидатор подставится. В поле `validator_options` Можно переопределять опции из дефолтного валидатора.
    * Перешли от списка versions к строчке version, перешли от уникальности ключа в конфиге к уникальности пары `(key, version)`. 
    * Новое поле `owners`. Для регулярных моделей со стафа подгружаются логины в телеграме овнеров и присылаются в алертах для быстрой связи.
    * Новое поле `tags`. 
    * Новое поле `life` для создания алертов на свежесть регулярных моделей. Содержит словарь из опциональных полей `update_time` -- максимальное время с момента публикации последнего valid ресурса и `version_lag` -- максимальная разница между текущей датой и версией модели.
    * Поле `deploy` deprecated. Для добавления матрикснета в движок нужно использовать поле deploy_bs, внутри которого лежит словарь с полем `mx_id`.
- __0.1.3__ Добавлена возможность указывать тип ресурса валидатора через `resource_type`
- __0.1.2__ Новое поле `deploy`, в котором одно возможное значение __bs__. Если оно указано, необходимо указать словарь `meta`, в котором указать список `MXID`.
- __0.1.1__ Новое поле `meta` с `format_version` внутри для поддержки версионированности конфига.
- __0.1.0__ Конфиг с фильтром версий и валидацией моделей.
