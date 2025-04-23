## Специальные возможности

В рамках проекта делаем возможность выбора доп. возможностей
для людей с ограниченными возможностями

Что значит «Специальные возможности»?
Опция «Помочь что-то загрузить», «Встретить», «Помочь посадить». Для людей с особенностями здоровья.

Зачем - опции в приложении не адаптированы к пользователям с особыми пожеланиями.

## Отображение на клиенте

Список спец. возможностей, предлагаемых к выбору

![image](static/special_features.png)

Есть возможность дать текстовое пояснение по некоторым пунктам

![image](static/special_feature_question.png)

Если нажать на темное поле / мисклик, экран закрывается.
Есть возможность нажать "Сохранить", если комментарий не заполнен.

При вводе комментария в этом поле разворачивается вьюшка

![image](static/special_feature_question_full.png)


Переходы к выбору спец. возможностей на клиенте возможны из заказа

![image](static/enter_from_order.png)

Необходимо также, на окне заказа, визуально помечать на клиенте факт того,
что что-то из спец. возможностей было выбрано, указывая количество выбранных опций

![image](static/special_features_count.png)

При селекте спец. возможности, если она имеет поясняющую коммуникацию, клиент должен показать её

![image](static/special_feature_explanation.png)


## Техническая реализация

### Клиент

Клиент должен уметь:
1. Сохранять в local storage все выбранные опции
2. Уметь так же сохранять доп. комментарий для опций, у которых есть ключ comment в local storage
3. Показывать фулскрин-коммуникацию при пселекте опции для опций с ключом communication

#### Спец. возможности в разделе заказа

Если клиент поддерживает группировку полей для пожеланий, в запрос 3.0/zoneinfo клиент отправляет новый элемент
"grouped_requirements" в массив supported. Если ключ не приходит, бэкенд возвращает ключ requirement_groups как раньше.

Если ключ пришел, формат ответ бэкенда менятеся

Было:

```json
{
  "requirement_groups": [
    {
      "title": "", // никогда не приходит с бэка, т.к. таск был не сделан
      "indices": [
        0,
        1,
        2,
        3,
        4
      ]
    }
  ],
  "supported_requirements": [
    {
      "default": false,
      "driver_name": "animaltransport_v2",
      "label": "Pet transportation",
      "name": "animaltransport",
      "type": "boolean"
    },
    {
      "default": false,
      "driver_name": "bicycle",
      "label": "Bicycle",
      "name": "bicycle",
      "type": "boolean"
    }
  ]
}
```

// Стало

```json
{
  // ...
  "max_tariffs": [ {
    // ..
    "view_sections": [ // Описывает вид секций, порядок секций и вложенных элементов
      {
        "title": "", // Заголовок секции(опциональный)
        "items": [ // Массив ссылок на элементы (group(в т.ч виртуальные) или requirement), которыми заполняем секцию
          {
            "name": "specials",
            "type": "group" // ищем в группах, которые создали из group_definitions по name
          },
          {
            "name": "conditioner",
            "type": "requirement"
          },
          {
            "name": "nosmoking",
            "type": "requirement" // ищем в supported_requirements по name
          },
          {
            "name": "$ungrouped_items", // Используем вирутальную группу
            "type": "virtual_group"
          }
        ]
      }
    ],
    "group_definitions": [ // Массив определений групп
        /*
          ungrouped_requirements виртуальная группа(не присылаем с бэкенда, имя можнет быть использовано в view_sections),
          содержит в себе все requirements из supported_requirements: [], которые не содержит ни одна другая группа
        */
        {
          "name": "$ungrouped_requirements", // Хардкодим имя на уровне API, не используем для кастомных групп
          "requirements": [], // Всегда пустой подразумеваем на уровне API, что тут все которые не попали ни в одну группу
          "grouping_type": "flat" // Тип группировки enum: [flat|item]
          // item - представляет группу в виде нового элемента, по тапу на который эта группа будет представлена
          // flat - представляет группу в виде неразврывной упорядоченной группы пожеланий
        },
        /*
          top_group - виртуальная группа (не присылаем с бэкенда, имя не должно присутствовать в view_sections)
          Содержит в себе все захаркоженные элементы, которые не были указаны явно в определнии другой группы
          Всегда располагается выше других секций в view_sections.
          Если все элементы были определны в других группах, т.е эта группа пустая - соответсвующая секция не будет отображена

          Вот их список(нужно дополнить):
          driver_instruction - комментарий водителю
          order_for_someone_else - заказать другому
          schedule_ride - запланировать поездку
        */
        {
            "name": "$top_group",
            "requirements": [],
            "grouping_type": "flat"
        },
        {
            "name": "specials",
            "title": "Специальные возможности",
            "subtitle": "Например, помощь с посадкой",
            "grouping_type": "item",
            "requirements": [
                "guide_dog",
                "need_empty_trunk"
            ],
            "presentation": {
                "type": "modal",
                "modal": {
                    "title": "Что сообщить водителю?",
                    "image_tag": "Тут_тег_картинки_с_сердечком",
                    "preview": "За эти пожелания вам не нужно доплачивать",
                    "button_text": "Готово"
                }
            },
            "bubble": {
                "title": "Специальные возможности"
            }
        }
    ],
    "supported_requirements": [
        {
            "default": false,
            "driver_name": "nosmoking",
            "label": "Некурящий салон",
            "name": "nosmoking",
            "type": "boolean"
        },
        {
            "default": false,
            "driver_name": "conditioner",
            "label": "Кондиционер",
            "name": "conditioner",
            "type": "boolean"
        },
        {
          "default": false,
          "driver_name": "guide_dog",
          "label": "Перевозка собаки-поводыря",
          "name": "guide_dog",
          "type": "boolean",
          "communication": {
              "id": "123456",
              "show_count": 1,
              "fallback": {
                  "title": "Как перевозить собак-поводырей",
                  "subtitle": "Захватите для собаки покрывало или плёнку и посадите её в ноги.",
                  "button_text": "Хорошо"
              }
          }
        },
        {
          "default": false,
          "driver_name": "need_empty_trunk",
          "label": "Нужен пустой багажник",
          "name": "need_empty_trunk",
          "type": "boolean",
          "communication": {
              "id": "123456",
              "show_count": 1,
              "fallback": {
                  "title": "Зачем нужен пустой багажник?",
                  "subtitle": "Например, положить туда инвалидное кресло",
                  "button_text": "Готово"
              }
          },
          "comment": {
              "placeholder": "Жду у остановки, в руках белая трость",
              "save_text": "Сохранить для следующих поездок",
          }
        }
    ]
    // ...
  }]
}
```

Сбор требований в секции происходит обходом элементов массива view_sections[i].items. Если тип элемента == group,
добавляем элементы в группу, путем матчинга поля name с элементом из group_definitions и дальнейшим обходом массива
requirements из group_definitions, чтобы выбрать нужные элементы из supported_requirements.

Для grouping_type == item обязательными являются поля title и presentation. Для flat клиент на эти поля не смотрит.

Если хотя бы одно из этих требований выбрано, к полю "Специальные возможности" (в нашем случае)
добавляется цифра - количество выбранных опций (см. картинку).

Если требования не выбраны, subtitle к пункту опций "Специальные возможности" берется из requirement_groups.subtitle.
При выборе каких-то опций subtitle заменяется на выбранные опции (см. картинку)

Если элемент массива имеет ключ comment, то, при свиче, открываем доп. окошко для комментария с плейсхолдером (см. картинку).
При тапе на окошко для комментария разворачивается вьюшка полного комментария (см. картинку).
Если в поле ввода комментария ставится галочка в поле "Сохранить для всех следующих поездок", то сохраняем комментарий в local storage

Если поле имеет коммуникацию (ключ communication), то показываем фулскрин по id, указанный в ключе id (см. картинку).
Фулскрин должен быть показан столько раз, сколько указано в настройке show_count. Если не удалось прогрузить фулскрин
показываем fallback, используя ключ communication.fallback

При сохранении черновика в ручке /3.0./orderdraft, если есть комментарии к опциям,
клиент дополнительно отсылает ключ requirements_additional_info, где ключ - название опции, значение - объект вида доп_свойство_опции: значение

Было:
```json
{
    "requirements": {
        "animal": true,
        "child": true,
        "guide_dog":  true,
        "need_empty_trunk": true,
        "childchair": 3
    }
}
```
Стало:
```json
{
    "requirements": {
        "animal": true,
        "child": true,
        "guide_dog":  true,
        "need_empty_trunk": true,
        "childchair": 3
    },
    "requirements_additional_info": {
        "need_empty_trunk": {
            "comment": "Буду в белом платье"
        },
        "guide_dog": {
            "comment": "Серая собака"
        }
    }
}
```

### Бэкенд

#### Эксперимент

Заводим эксперимент requirement_groups, где будем перечислять требования, которые нужно сгруппировать,
а также танкерные ключи для заголовка, подзаголовка и модалки

Пример json'а эксперимента

```json
{
  "view_sections": [
    {
      "title": "Название группы опций",
      "items": [
        // Для структуры айтемов можно использовать OneOf, и при необходимости расширять новыми объектами
        {
          "type": "group",
          "name": "specials",
          "title": "Специальные возможности",
          "subtitle": "Например, помощь с посадкой",
          "grouping_type": "item",
          "requirements": [
            "guide_dog",
            "need_empty_trunk"
          ],
          "presentation": {
            "type": "modal",
            "modal": {
              "title": "Что сообщить водителю?",
              "image_tag": "Тут_тег_картинки_с_сердечком",
              "preview": "За эти пожелания вам не нужно доплачивать",
              "button_text": "Готово"
            }
          },
          "bubble": {
            "title": "Специальные возможности"
          }
        }
      ]
    }
  ]
}
```

Где: </br>
**title** - optional string, название для группы опций </br>
**items** - required array[mixed], массив, описывающий группу опций </br>
**items[i].type** - required string, тип элемента. Может быть один из: group - слитые опции вместе, requirement - отдельная опция,
virtual_group - особый тип для виртуальных групп ($top_group и $ungrouped_requirements) </br>
**items[i].name** - required string, название группы, с которой будет происходить матчинг </br>
**items[i].title** - optional string, заголовок для сгруппированных опций
**items[i].subtitle** - optional string, подзаголовок для сгруппированных опций
**items[i].grouping_type** - required string, тип группировки. Может быть один из:
item - представляет группу в виде нового элемента, по тапу на который эта группа будет представлена,
flat - представляет группу в виде неразврывной упорядоченной группы пожеланий </br>
**items[i].requirements** - required array[string]. Массив из списка требований. Может быть пустым </br>
**items[i].presentation** - optional object. презентация для типа group (Модалка или что-нибудь еще в будущем) </br>
**items[i].presentation.type** - optional string Тип презентации. На данный момент только modal </br>
**items[i].presentation.modal** - optional object объект, описывающий модальное окно, при клике на сгруппированные опции </br>
**items[i].presentation.modal.title** - optional string Заголовок модального окна </br>
**items[i].presentation.modal.image_tag** - optional string Тэг картинки, которая будет вставлена слева от превью в модальном окне</br>
**items[i].presentation.modal.preview** - optional string Превью модального окна </br>
**items[i].presentation.modal.button_text** - optional string Текст на кнопке в модальном окне </br>
**items[i].bubble** - optional object Объект бабла для типа group </br>
**items[i].bubble.title** - optional string Текст на бабле </br>

Хранение спец. возможностей будет осуществляться в монге requirements, но при сохранении добавлются новые поля

```json
{
    "comment": {
      "placeholder": "special_features.need_empty_trunk.comment.placeholder",
      "save_text": "special_features.modal.save_text"
    },
    "communication": {
        "id": "123456",
        "show_count": 1,
        "fallback": {
          "title": "special_features.need_empty_trunk.communication.fallback.title",
          "subtitle": "special_features.need_empty_trunk.communication.fallback.subtitle",
          "button_text": "special_features.need_empty_trunk.communication.fallback.button_text"
        }
    }
}
```

Где: </br>
**comment.placeholder** - optional string, плейсхолдер в окошке комментария (танкерный ключ) </br>
**comment.save_text** - optional string, текст "Сохранить для следующих поездок" в окошке комментария (танкерный ключ) </br>
**communication.id** - optional string, id фулскрина-коммуникации </br>
**communication.show_count** - optional int, количество показов коммуникации</br>
**communication.fallback.title** - optional string, тайтл для фалбэка коммуникации (танкерный ключ) </br>
**communication.fallback.subtitle** - optional string, сабтайтл для фалбэка коммуникации (танкерный ключ) </br>
**communication.fallback.button_text** - optional string, текст кноки для фалбэка коммуникации (танкерный ключ) </br>

#### Админка

##### Раздел "Требования"

В админке, в разделе "Требования" нужна доработка со стороны фронта. Добавляются следующие поля:

"ID онбординг коммуникации" - optional string </br>
"Количество показов онбординг коммуникации" - optional int (required, если указан ID онбординг коммуникации) </br>
"Заголовок для fallback онбординг коммуникации" - optional string (required, если указан ID онбординг коммуникации) </br>
"Подзаголовок для fallback онбординг коммуникации" - optional string (required, если указан ID онбординг коммуникации) </br>
"Текст кнопки для fallback онбординг коммуникации" - optional string (required, если указан ID онбординг коммуникации) </br>
"Плейсхолдер комментария" - optional string </br>
"Текст сохранения в комментарии" - optional string </br>

При отправке данных в PUT api-запрос /v2/requirements/{name} в сервис requirements
для этих полей используются ключи

```yaml
    comment:
        type: object
        properties:
            placeholder:
                type: string
            save_text:
                type: string
    communication:
       type: object
       properties:
          id:
            type: string
          show_count:
            type: int
          fallback: object
          properties:
            title:
              type: string
            subtitle:
              type: string
            button_text:
              type: string
```

#### userstate

В ответе userstate нужно отдавать новый ключ requirements_additional_info, который клиент присылает в orderdraft

```json
{
    "requirements_additional_info": {
        "need_empty_trunk": {
            "comment": "Буду в белом платье"
        },
        "guide_dog": {
            "comment": "Серая собака"
        }
    }
}
```

#### Таксометр
Добавляется новый ключ в order_proc.order.request.requirement_objects

Было:
```json
{
    "requirements": {
        "animal": true,
        "child": true,
        "guide_dog":  true,
        "need_empty_trunk": true
    }
}
```
Стало:
```json
{
    "requirements": {
        "animal": true,
        "child": true,
        "guide_dog":  true,
        "need_empty_trunk": true,
        "childchair": 3
    },
    "requirement_objects": [
        {"name": "animal",  "value": true},
        {"name": "child", "value": true},
        {"name": "guide_dog", "value":  true},
        {"name": "childchair", "value": 3},
        {"name": "need_empty_trunk", "value" : true, "comment": "нужен пустой багажник"}
    ]
}
```

Новое поле comment добавляется к водительскому комментарию по шаблону (если есть комментарий к опции)
"Опция 1 (коммент к опции 1), Опция 2 (коммент к опции 2)".
Пример:
Помогите мне дойти до машины (буду в белом платье)



