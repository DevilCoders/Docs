### Описание
Добавляем к тарифу "Доставка"("Курьер") опцию от двери до двери.
Опция тянет за собой дополнительные поля для всех точек маршрута (на данном этапе только A и B):
- этаж
- квартира
- телефон получателя/отправителя из телефонной книги
- ФИО получателя/отправителя (пока под вопросом)
Все эти данные нужно передать водителю, чтобы он мог доставить посылку в буквальным смысле от двери до двери (как это обычно происходит при курьерской доставке).
Все это потребует нового UI для доп. информации по заказу на клиентах и таксометре.
[Тикет](https://st.yandex-team.ru/TAXIBACKEND-24626)  


### Гипотеза:
Данная доработка позволит нам выйти на рынок e-commerce, что в свою очередь позволит повысить количество заказов.
Конкретные метрики оптимизировать не будем, AB тестирование не проводим - бизнес верит в то, что фича крайне важна и поможет заработать много денег в будущем. 
Но будем следить за конверсией и количеством заходов в тариф доставка. 
Текущие метрики: [графана](https://grafana.yandex-team.ru/d/uDh15VvZz/taxi-delivery-tariff?orgId=1), [дашборд статистики](https://dash.yandex-team.ru/jyewitasmfc0g?state=e3ba0e051109)


### Дизайн
[Дизайн в фигме со схемой флоу создания заказа](https://www.figma.com/file/TZMNVE3YzGBElriZQNKlOZcr/%D0%A2%D0%B0%D1%80%D0%B8%D1%84-%C2%AB%D0%94%D0%BE%D1%81%D1%82%D0%B0%D0%B2%D0%BA%D0%B0%C2%BB?node-id=1905%3A23855)


### Продуктовые ограничения

Основные ограничения:
- не можем заложить в UI поля точного адреса на все случаи жизни (этот недостаток комментируем комментарием для каждой точки маршрута)

Как минимум на первых этапах также имеем следующие ограничения: 
- в маршруте может быть только 1 точка назначения (не доставляем по 2 и более адресам)
- не передаем на таксометр контактное имя
- не делаем подтверждения получения заказа 
- фиксированная стоимость требования "от двери до двери"


## Архитектура
### Проблемы которые нужно решить
1) Передать на клиент параметры верстки (поля и их порядок отображения, титулы, иконки)
2) Передача (с клиента на бэк и обратно) и хранение вместе с адресом дополнительных полей:
- этаж
- квартира
3) Передача (с клиента на бэк и обратно) и хранение информации о третьих лицах (принимающих и отправляющих грузы):
- телефон
- фио,
- биндинг с адресом.
4) Передача на таксометр доп. информации для каждой точки:
- телефон
- фио 
- адрес с этажом и квартирой
ФИО - пока под вопросом, на первых этапах не передаем 

### Решение

#### Этап 1 (сделано)
В качестве очень быстрого решения используем комментарий к заказу как способ доставки точного адреса для опции "от двери до двери"

##### protocol
Добавляем новый тип ошибки 406 в ответе _/ordercommit_:
```(json)
{
  "error": {
    "code": "COMMENTS_REQUIRED",
    "text": "Для доставки от двери до двери в комментариях необходимо указать точный адрес"
  }
}
```
Также убираем сохранение комментария для адреса в случае "от двери до двери" 
Закрываем все экспериментом (и ставим задачу на удаление этого куска кода в будущем)

#### Этап 2 
MVP с реализацией полноценного UI на клиентах и таксометре. 
Доставляем от пользователя до водителя информацию об этаже, квартире, контактном телефоне, доп. комментарии. 

##### Клиенты (protocol)
На данном этапе мы хардкодим UI и его логику на клиентах. 
Через эксперимент в _/zoneinfo_ прокидываем на клиенты строки локализации всех необходимых элементов - 
для этого потребуется там же подставлять в результат эксперимента перевод танкерных ключей.
API в эксперименте _/zoneinfo_:
```(json)
{
  "name": "route_additional_information_step",
  "value": {
    "enabled": true,
    "tariffs": [
      "express"
    ],
    "turn_on_requirement_notification": {
      "description": "Донести до квартиры - платно"
    },
    "continue_with_requirement_alert": {
      "cancel_button_text": "Ввести номер квартиры",
      "continue_button_text": "Продолжить без номера",
      "description": "Можно и без него - но тогда водитель позвонит, чтобы уточнить адрес",
      "title": "Не хватает номера квартиры"
    },
    "title": "Кому и от кого",
    "price_label": "Стоимость",
    "dependant_boolean_requirement": "door_to_door",
    "points": [
      {
        "type": "source",
        "label": "Кто отправит",
        "title": "От кого и откуда забрать",
        "placeholder": "Укажите",
        "options": [
          {
            "type": "phone_number",
            "name": "contact_phone", // можно не присылать с сервера, зашиваем на клиенте
            "label": "Кто отдаст посылку водителю",
            "phone_required_popup_properties": {
              "button_text": "Хорошо",
              "description": "Уточните, от кого доставка",
              "title": "Кто отдаст посылку водителю"
            },
            "phone_selection_screen": {
              "title": "Кто отправит",
              "read_contacts_permission": "Разрешите доступ к контактам для выбора отправителя",
              "choose_one_label": "Выберите номер телефона"
            }
          },
          {
            "type": "apartment_info",
            "name": "apartment_info", // можно не присылать с сервера, зашиваем на клиенте
            "apartment_key": "apartment", // можно не присылать с сервера, зашиваем на клиенте
            "apartment_label": "Квартира, офис",
            "floor_key": "floor", // можно не присылать с сервера, зашиваем на клиенте
            "floor_label": "Этаж"
          },
          {
            "type": "comment",
            "name": "comment", // можно не присылать с сервера, зашиваем на клиенте
            "label": "комментарий"
          }
        ]
      },
      {
        "type": "destination",
        "label": "Кто заберёт",
        "title": "Кому и куда отвезти",
        "placeholder": "Укажите",
        "options": [
          {
            "type": "phone_number",
            "name": "contact_phone", // можно не присылать с сервера, зашиваем на клиенте
            "label": "Кто получит посылку",
            "phone_required_popup_properties": {
              "button_text": "Хорошо",
              "description": "Уточните, для кого доставка",
              "title": "Кто заберет посылку у водителю"
            },
            "phone_selection_screen": {
              "title": "Кто заберет",
              "read_contacts_permission": "Разрешите доступ к контактам для выбора получателя",
              "choose_one_label": "Выберите номер телефона"
            }
          },
          {
            "type": "apartment_info",
            "name": "apartment_info", // можно не присылать с сервера, зашиваем на клиенте
            "apartment_key": "apartment", // можно не присылать с сервера, зашиваем на клиенте
            "apartment_label": "Квартира, офис",
            "floor_key": "floor", // можно не присылать с сервера, зашиваем на клиенте
            "floor_label": "Этаж"
          },
          {
            "type": "comment",
            "name": "comment", // можно не присылать с сервера, зашиваем на клиенте
            "label": "комментарий"
          }
        ]
      }
    ]
  }
}
```
Для каждой точки в маршруте добавляем в тело запроса ручки _/orderdraft_ поля _floor_, _apartment_, _contact_phone_, 
которые будем сохранять в _order_proc_:
```(json)
{  
  route:[
    {
      "extra_data":{ 
        "contact_phone": "контактный телефон",        
        "floor": "этаж",
        "apartment": "квартира",
        "porch": "подъезд",
        "comment":"Комментарий"
      },
      ...
    },
    ...
  ],
  ...
}
```

Изменение в коллекции order_proc:
```(json)
{  
  "order" : {
    "request" : {
      "source" : {
        "extra_data":{                                         
          "floor": "этаж",
          "apartment": "квартира",
          "porch": "подъезд",
          "comment":"Комментарий"
        }
      },
      "destinations" : [
        {
          "extra_data":{                                         
            "floor": "этаж",
            "apartment": "квартира",
            "porch": "подъезд",
            "comment":"Комментарий"
          },
          ...
        },
        ...       
      ], # destinations
      ...
    }, # request
    ...
  }, # order
  ...
}
```


#### Такcометр (processing + protocol)
На таксометр необходимо пробрасывать телефон, этаж и квартиру для каждой точки маршрута. 
Со стороны клиентского бэка пробрасываем из _order_proc_ в _setcar_ этаж и квартиру:
```(xml)
<Request>
  <Source>
    <ExtraData>
      <Floor>этаж</Floor>
      <Apartment>квартира</Apartment>
      <Porch>Подъезд</Porch>
      <Comment>Комментарий</Comment>    
    </ExtraData>    
    ...
  </Source>
  <Destinations>
    <Destination order="1" arrival_distance="100">
      <ExtraData>
        <Floor>этаж</Floor>
        <Apartment>квартира</Apartment>
        <Porch>Подъезд</Porch>
        <Comment>Комментарий</Comment>    
      </ExtraData>   
    ...
    </Destination>
    ...
  </Destinations>
</Request>
```
Телефоны для точек A и B пробрасываются через _/requestconfirm_ (доработка не требуется)  

#### Этап 3 (и последующие этапы)
(Здесь представлен примерный перечень задач. Этот этап будем прорабатывать отдельно после завершения этапа 2)
На данном этапе:
 - убираем хардкод UI на клиентах (реализуем его гибкую настройку)
 - сохраняем на бэке однажды введенные доп.данные по адресам и третьим лицам, чтобы пользователь мог ими воспользоваться

#### Гео (_userplaces_ + _persuggest_)
В сервисе _userplaces_ добавляем в ручки _/3.0/userplaces, /3.0/userplacesupdate, /userplaces/item, /userplaces/list, /v1/takeout_ и в коллекцию _user_places_ следующие поля:
```(json)
одно место пользователя (консистентно для ответов/запросов всех ручек и бд)
{
  extra_data":{
    "floor": "этаж",
    "apartment": "квартира",
  },
  ...
}
```
В сервисе _persuggest_ добавляем в ответ ручек _/zerosuggest_ и _/suggest_ аналогичные поля:
```(json)
{
  "results": [
    {
      extra_data":{
        "floor": "этаж",
        "apartment": "квартира"
      },
      ...
    }
  ],
  ...
}
```
Пока эти поля получится заполнять только для адресов из _userplaces_. 
В дальнейшем планируется аналогичная доработка для адресов из истории заказов (сейчас хранится в _phone_history_), 
которая будет включать в себя:
- создание отдельного сервиса для организации взаимодействия с сущностью _phone_history_
- доработку в _ML_
- доработку в _persuggest_

#### Сервис дополнительной информации по заказу (временное название order-additional-info)
С одной стороны нам нужно уметь гибко настраивать UI доп. шагов формирования требований к заказу, 
с другой стороны необходимо хранить и обрабатывать эту доп информацию сервисами с соответсвтующей специализацией.
Таким образом нам необходим сервис, который будет решать следующие задачи:
- форимрование структуры (и логику) UI клиентов для доп требований заказа (нужны соответствующие ручки для админки)
- отдавать эту струкруту UI на клиенты (ручка в которую будем ходить из proxy-zoneinfo в proxy-api)
- (?) диспетчеризовать доп.данные по заказу между соответствующими сервисами (из /orderdraft ставим stq-таску в аргументы которой передаем доп. данные по заказу, при исполнении которой будем передавать данные заинтересованным сервисам в соответствии с некоторой заданной в админке конфигурацией)
данные между

#### Сервис door-to-door (?)
Для выноса доп данных по заказам door_to_door из коллекции order_proc возможно нам потребуется создать отдельный сервис, который будет хранить эти данные.

#### Клиенты (protocol)
Дорабатываем /routestats  аналогично тому, как доработали в предыдущем этапе /orderdraft - пробрасываем ту же доп. информацию по каждой точке маршурта
(это может понадобится в будущем для гибкой тарификации, но пока не актуально).

Пробрасываем в ответ ручек _3.0/suggest, 3.0/suggestedpos, 3.0/suggesteddest_ 
(последние две ручки в ближайшем будущем переезжают из протокола в _persuggest_) 
поля _floor_ и _apartment_ из соответствующих ручек сервиса _persuggest_:
```(json)
одно место пользователя
{
  extra_data":{
    "floor": "этаж",
    "apartment": "квартира",
  },
  ...
}
```
Заменяем эксперимент в _/zoneinfo_ на API в отдельной ручке отдельного микросервиса order-additional-info (см выше)
(который бедет отвечать за форимрование доп шагов UI в тарифе)
Переводим _/zoneinfo_ на api-proxy, в котором будем подмешивать новую часть API из order-additional-info.
Примерный вид API в proxy-zoneinfo:
```(json)
{ 
  ...
  "max_tariffs":[
    {
      ...
      "max_route_points_count": 1,  # Максимальное количество точек назначения (уже существующее поле) 
      "supported_requirements":[
        {
          "type": "boolean",
          "name": "door_to_door",
          "label": "От двери до двери",
          "default": false,
          "persistent": false,
          "independent_tariffication": true
        },
        ...
      ],
      "order_additional_steps":[ # Дополнительные шаги (экраны) для формирования параметров заказа 
        {
          "type": "additional_summary", # Тип - доп. саммари (попадаем по кнопке "заказать")      
          "name": "express_additional_summary",
          "title": "Кому и от кого",
          "price_label": "Стоимость",
           # порядок элементов в верстке на промежуточном экране для тарифа доставка 
          "layout":[            
            {"type": "price"},                      # цена
            {
              "type": "additional_step",            # дополнительный шаг формирования параметров заказа  
              "name": "source_additional_info"      # доп. информация для точки A (определяется по полю name в additional_steps) 
            },      
            {
              "type": "additional_step",            # дополнительный шаг формирования параметров заказа
              "name": "destination_additional_info" # доп. информация для точки B
            },
            {
              "type": "requirement", 
              "name": "door_to_door"                # требование "от двери до двери"
            }
          ]
        
          "order_additional_steps":[ # Дополнительные подшаги
            {
              "type": "templated_step" # Тип определяется шаблоном
              "template": "express_additional_info", # шаблон дополнительного экрана (определяется по полю name в additional_step_templates) 
              "name": "source_additional_info",
              "template_params":{ # параметры шаблона
                "point_type": "source" # тип точки маршрута к которой привязываем этот дополнительный экран
              },
              "l10n":{ # Словарь локализации
                "phone_label": "Укажите телефон отправителя",
                ...
              },
              "label": "Кто отправит?", # наименование этого доп.шага на экране доп.саммари
              "icon": {  # иконка этого доп.шага на экране доп.саммари
               ... # заполняется аналогично остальным картинкам
              },
            },
            { # аналогично
              "type": "templated_step"
              "template": "express_additional_info",
              "name": "destination_additional_info",
              "template_params":{
                "point_type": "destination" 
              },
              "l10n":{ 
                "phone_label": "Укажите телефон получателя",
                ...
              },
              "label": "Кому доставить?",
              "icon": { 
               ... 
              },
            }
          ], # express_additional_summary.additional_steps.
        },  # express_additional_summary
        ...
      ], # additional_steps
      notifications:[
        {          
          "type": "simple_notification", # тип нотификации
          "name": "door_to_door_notification", 
          "description": "Донести до квартиры - платно",          
        },
        {
          "type": "continue_alert",
          "name": "door_to_door_continue_alert",
          "title": "Не хватает номера квартиры"
          "description": "Можно и без него - но тогда водитель позвонит, чтобы уточнить адрес",
          "continue_button_text": "Продолжить без номера",
          "cancel_button_text": "Ввести номер квартиры"
        }      
      ], # notifications
      clauses:[ 
        {
          "predicate": {
            "type": "all_of", # Условие выполняется если истинны все значения в args 
            "args":[
              {
                "type": "any_of" # Условие выполняется если истинны хотя бы одно значение в args 
                "args":[
                  {
                    "type": "field_used" # true если поле использовано
                    "arg": "express_additional_summary.additional_steps.source_additional_info.floor"
                  },
                  {
                    "type": "field_used",
                    "arg": "express_additional_summary.additional_steps.source_additional_info.apartment"
                  },
                  {
                    "type": "field_used" 
                    "arg": "express_additional_summary.additional_steps.destination_additional_info.floor"
                  },
                  {
                    "type": "field_used",
                    "arg": "express_additional_summary.additional_steps.destination_additional_info.apartment"
                  }
                ]
              },
              {
                type": "not", # логическое НЕ
                "args":[
                  {
                    "type": "requirement_value" # вернуть значение в требовании
                    "arg": "door_to_door" # имя требования                    
                  }
                ]
              },
            ]
          }
          "set": [ # установить какие-либо значения (выполняем если выполняется условие в predicate)
            {
              "type": "requirement",
              "name": "door_to_door",
              "value": true           # установить значение "door_to_door" в true
            }
          ]
          "show_notification": "door_to_door_notification" (показываем если выполняется условие в predicate)
        },
        {
          "predicate":{
            "type": "all_of"
            "args": [
              {
                "type": "any_of"
                "args":[
                  {
                    "type": "not", # логическое НЕ
                    "arg:{
                      "type": "field_used",
                      "arg": "express_additional_summary.additional_steps.source_additional_info.apartment"
                    }
                  },
                  {
                    "type": "not", # логическое НЕ
                    "arg:{
                      "type": "field_used",
                      "arg": "express_additional_summary.additional_steps.destination_additional_info.apartment"
                    }
                  }
                ]
              },
              {
                "type": "requirement_value",
                "arg": "door_to_door"
              }
            ]
          },
          "show_notification": "door_to_door_continue_alert"
        },
        {
          # аналогично можно добавить нотификацию при незаполненном этаже
          ...
        }
      ] # clauses 
    },
    ...
  ], # max_tariffs
  "templates":[
    {
      "type": "route_point_additional_info", # тип доп.шага, привязанного к точке маршрута
      "name": "express_additional_info",  # имя шаблона для доставки
      "title": "express_additional_info_title" # "Отправить посылку" (ключ секции l10n)
      
      # порядок верстки на экране с доп опциями для точки маршрута 
      "layout":[
        {
          "type": "option",
          "name": "contact_phone"
        },
        {
          "type": "option",
          "name": "contact_name" 
        },
        {
          "type": "divider",
        },
        {
          "type": "route_point",
        },
        {
          "type": "option",
          "name": "apartment_info"
        },
        {
          "type": "option",
          "name": "comments"
        },
        {
          "type": "price_label",
        }
      ],
      options":[
        {
          "type": "phone_number", # дополняем адрес номером телефона
          "name": "contact_phone",
          "label": "phone_label", # "Кому доставить"  (здесь и далее это ключ секции l10n)         
          "selected_label": "phone_select_label" # "Получит" - отображение требования после того, как выбран телефон
          "required": true,  # необходимость указать поле во время заказа
          "phone_required_popup_properties": {
              "button_text": "phone_popup_button_text" #  "Хорошо",
              "description": "phone_popup_description" # "Уточните, кому доставка",                
              "title": "contact_phone_popup_title"
          },            
          # Получит +X(XXX)XXX-XX-XX
          "phone_selection_screen": {
              "title": "phone_selection_screen_title"  # "Кому отправляете?",
              "read_contacts_permission": "phone_selection_screen_permission" # "Разрешите доступ к контактам для выбора получателя",
              "choose_one_label": "phone_selection_screen_choose_one" # "Выберите номер телефона",
          }
        },
        {
          "type": "person_name", # дополняем адрес именем человека (пока не реализуем, но закладываемся на будущее)
          "name": "contact_name",
          "label": "contact_name_label" # "Как представить получателя водителю",
        },
        {
          "type": "apartment_info", # дополняем адрес этажом и номером квартиры/офиса
          "name": "apartment_info",
          "apartment_key": "apartment" # ключ поля apartment
          "apartment_label": "apartment_label" # "Квартира, офис",
          "floor_key": "floor" # ключ поля floor
          "floor_label": "floor_label" # "Этаж",
        }, 
        {
          "type": "comment", # дополняем адрес комментарием
          "name": "comment",
          "label": "comment_label" # "комментарий"
        }
      ], # options
    }, 
    ...
  ], # additional_step_templates
  ...
}
```

#### Хранение информации о третьих лицах
Нужен сервис (скорее всего будем дорабатывать сервис персональных данных), который будет хранить  информацию о третьих лицах
Хранить будем примерно так:
```(json)
{
  "user_id": "id пользователя",
  "third_person_phone": "телефон третьего лица, введенный пользователем",
  "third_person_name": "имя третьего лица, введенное пользователем",
  "user_place_id": "идентификатор места пользователя из userplaces"
}
уникальный ключ по (user_id, third_person_phone)
```

### Этапы и оценки сроков

#### Этап 1
Временный костыль в _protocol_:
- [2d] _/ordercommit_ (новое сообщения в ответе 406 + отвязываем коммент от адреса)
- [2d] _/zoneinfo_  (реализуем возможность выключать новые требования в тарифе по эксперименту)
Итого: 4д + запас = 5д

#### Этап 2
Делаем новый экран для тарифа "Доставка", но пока не запоминаем дом и этаж (в _userplaces_), и не запоминаем информацию о третьих лицах.
Доработка в _protocol_:
- [3d] _/orderdraft_
- [3d] _/zoneinfo_
Доработки в процессинге:
- [2d] передавать новую информацию в setcar
Итого: 8d + запас = 10d

#### Этап 2.1 (тех долг)
Доделываем то что не успевали сделать на этапе 2 в части динамической верстки UI.
Доработки в _protocol_:
- [0.5d] убираем следы этапа 1
- [?] что-то еще (?)

#### Этап 3 и последующие (очень примерные оценки)

##### Гео
Запоминаем на бэке в избранных адресах пользователя этаж и квартиру (все оценки лучше уточнить у @stepa_ma)
Доработки в _userplaces_:
- [1d] _/3.0/userplaces_
- [1d] _/3.0/userplacesupdate_
- [1d] _/userplaces/item_ 
- [1d] _/userplaces/list_ 
- [1d] _/v1/takeout_

Доработки в сервисе _persuggest_:
- [1d] _/zerosuggest_ 
- [1d] _/suggest_ 
- [1d] _3.0/suggestedpos_ (после переноса из протокола)
- [1d] _3.0/suggesteddest_  (после переноса из протокола)

Доработки в _protocol_:
- [1d] _3.0/suggest_ 

Запоминаем на бэке в истории последних адресов этаж и квартиру. Доработка возможна после создания отдельного сервиса для хранения информации по истории заказов.
Примерные оценки:
- [3d] правка ручек в сервисе истории заказов
- [2d] доработка в _persuggest_
Итого: 15d + запас = 19d

##### protocol
- [3d] перенос ручки /zoneinfo в api-proxy
- [1d] добавление API для door_to_door в новой /proxy-zoneinfo
Итого: 4d + запас = 5d

##### Сервис доп.данных заказа (рабочее название order-additional-info)
- [1d] накладные расходы на создание нового сервиса
- [5d] ручка админки для формирования структуры UI
- [2d] ручка для отдачи структуры UI в /proxy-zoneinfo 
- [?] диспетчеризация доп.данных заказа между ответственными сервисами
Итого: 8d + запас = 10d

##### Сервис door-to-door (если потребуется)
- [1d] накладные расходы на создание нового сервиса
- [2d] забрать данные по заказу
- [2d] отдать данные по заказу
- [2d] утилизация данных по старым заказам
Итого: 7d + запас = 9d

##### Данные о третьих лицах
- [2d] сбор информации из истории заказов
- [2d] ручка отдающая информацию по третьим лицам на клиент 
- [2d] передавать персональные данные в takeout
Итого: 6d + запас = 7d

#### int-api
[?] дорабатываем int-api
