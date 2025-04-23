### Описание
Запускаем новый тариф "Курьер": <br>
основное отличие тарифа от всех остальных - доп. поле "_кому доставка_", в которое пользователь записывает телефон получателя.

Ввод этого поля будет реализован со стороны клиентской разработки на основе того же компонента, что и 'отправка другому'

### Проблемы
1) Отдача пользователям конфигурации для отображения (как отображать, где брать тексты, обязательность доп. поля)
2) Передача поля в таксометр
3) Просмотр и отказ от каких-то лишних оповещений
4) Конфигурирование настроек

### Решение
#### Клиентский протокол
1) реализуем на основе требования "заказа другому", факты об этом требовании:
- это требование зашито на клиентах (реализовано **не** через requirements)
- на это требование может влиять флаг в ответе zoneinfo - _max_tariffs.$.order_for_other_prohibited_
- значение этого поля пробрасывается в orderdraft в поле _extra_contact_phone_
2) добавляем новый блок в zoneinfo:
```(json)
ответ zoneinfo
{
    ...
    "max_tariffs": [
    ...
        {
            ...
            "order_for_other_prohibited": true,  # важно запретить order_for_other
            "extra_contact_phone_rules": {
                "required": true,  # необходимость указать поле во время заказа
                "phone_required_popup_properties": {
                    "button_text": "Хорошо",
                    "description": "Уточните, кому доставка",
                    "title": ""
                },
                "requirement_label": "Кому доставить",  # название требования в списке требований
                "selected_label": "Получит",  # отображение требования после того, как выбран телефон
                # Получит +X(XXX)XXX-XX-XX
                "phone_selection_screen": {
                    "title": "Кому отправляете?",
                    "read_contacts_permission": "Разрешите доступ к контактам для заказа выбора получателя",
                    "choose_one_label": "Выберите номер телефона для заказа"
                }
            }
            ...
        }
    ...
    ]
    ...
}
```
3) клиенты слегка кастомизируют существующую логику заказа "для другого" и отправляют значение также в поле _extra_contact_phone_

**Чего мы лишаемся с таким флоу:**
мы не можем заказать курьера для другого человека, но кажется что  @kravchusha ок.
#### Таксометр
Описанная @kravchusha схема https://st.yandex-team.ru/TAXIMETERBACK-6353#5d124ecb874b2b0020b406f7:

**Блок Requestconfirm/setcar**
* Бэк такси отправляет в requestconfirm структуру phone_options: ```[{"type": "main", "label": "text1"}, {"type": "extra", "label": "text2"}]```// если массив из двух элементов то таксометр показывает диалоговое окно

_для обычных заказов phone_options:_ 
```(json)
[
  {
    "type": "main",
    "label": "Телефон пассажира"
  }
]
```
_для заказов, где есть доп телефон_
```(json)
заказ для другого: phone_options:
[
  {
    "type": "extra",
    "label": "Телефон пассажира"
  },
  {
    "type": "main",
    "label": "Если не смогли дозвониться"
  }
]

заказ тарифа курьер phone_options:
[
  {
    "type": "main",
    "label": "Отправитель"
  },
  {
    "type": "extra",
    "label": "Получатель"
  }
]
```
* Бэк таксометра проксирует этот параметр в setcar
* Таксометр получает параметр в setcar и в зависимости от пришедших типов отображает логику с нажатием на кнопку "Звонок"

**Блок Voiceforwarding**
* Таксометр отправляет в запросе нужный тип
```(json)
?order_id=xxx&...&type=main
```
* Бэк таксометра проксирует тип 
* Бэкенд такси (в зависимости от типа) берет из базы соответствующий телефон (не ломая шлюзы и переадресацию)
* [Переводим ручку voiceforwading](https://st.yandex-team.ru/TAXIBACKEND-23545) с xml ответа на json по хедеру Accept: application/json
по хедеру Accept: application/json
вместо xml ответа
```(xml)
<?xml version="1.0"?>
<Forwardings>
 <Forwarding>
  <Orderid>978c8824156e30deb5b98aa358828c8a</Orderid>
  <Phone>***</Phone>
  <Ext>***</Ext>
  <TtlSeconds>900</TtlSeconds>
 </Forwarding>
</Forwardings>
```
отдавать json
```(json)
{
  "forwardings": [
    {
      "order_id": "978c8824156e30deb5b98aa358828c8a",
      "phone": "***",
      "ext": "***",
      "ttl_seconds": 900
    }
  ]
}
```

-----------------
Обратная совместимость
Для старых клиентов, если в запросе не приходит тип, считается, что он main 

(проверить как сейчас на бэке такси валидируется заказ для другого- и для таких заказов считать что отсутствие параметра == extra)
#### Оповещения
Оповещения фиксятся с помощью
https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/NOTIFICATION_PREFIX_BY_TARIFF
#### Конфигурирование
необходимо конфигурировать следующие поля в зависимости от тарифа:
1) весь extra_contact_phone_rules
2) приоритет в ответе requestconfirm
3) label в requestconfirm

предлагается конфиг для хранения переводов
```(json)
FOR_ANOTHER_OPTIONS_BY_TARIFF (группа order_for_another)

{
  "__default__": {
    "required": false,
    "types_priority": [
        {
            "type": "extra",
            "weight": 1 # больше вес - раньше в массиве, по умолчанию у всех 0
            # если веса равны, то сортируем по 'type'
        }
    ]
  },
  "tariff_name": {
    "required": true,
    "tanker_prefix": "new_prefix",
    "types_order": [
        {
            "type": "main",
            "weight": 1
        }
    ]
  }
}

соответственно для всех ключей танкера заказа для другого по дефолту будет искаться
client_messages.for_another_requirement_label

в то время как для нового тарифа
client_messages.new_prefix.for_another_requirement_label
```