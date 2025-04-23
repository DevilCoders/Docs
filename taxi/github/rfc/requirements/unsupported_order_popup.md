### "Бабблы" выбранных пожеланий и отдельных опций (кресла в Детском, например)

![image](static/reqs_bubbles_1.png)

### Попап при неподдерживаемом пожелании

![image](static/order_popup_child.png)

#### Сценарий
Выбираем не-tariff_specific пожелание(я), переключаем на тариф где хотя бы одно пожелание недоступно
(также некоторые случаи tariff_specific пожеланий)

#### Как работает сейчас
Видим плашку "Сбросить недоступное пожелание" которая при нажатии сбрасывает выбор пожелания.
Кнопка заказа заблокирована, на ней соответствующий текст.
Надпись на недоступной кнопке заказа и собственно пожелание приходит в service_level-е
```
"service_levels": [
  {
    "class": "econom", ...
    "tariff_unavailable": {
      "code":"unsupported_requirement",
      "message":"В тарифе недоступно выбранное пожелание"
    },
    "unsupported_requirements":["childchair_moscow"]},
    ...
  },
  ...
]
```
Цена и ETA в соответствующих категориях не видна.

#### Что хотим
* Показывать ETA и цену с учетом только поддерживаемых требований
* Не блокировать кнопку заказа, показывать т.н. модальное окно

#### Изменения в zoneinfo
В клиентский эксперимент `requirements_v2` приходят параметры
* бабблов
* кнопки заказа и модального окна

_Если для требования пришли эти настройки, то клиент меняет плашку "Сбросить недоступные пожелания" на неблокирующую кнопку заказа и модальное окно._

```
{
  "l10n": [
      "requirement.ski.bubble": "Лыжи",
      "requirement.unsupported.order_button.one": "Уехать без $N$ пожелания",
      "requirement.unsupported.order_button.many": "Уехать без $N$ пожеланий",
      "requirement.unsupported.order_button.delivery.one": "Вызвать без $N$ пожелания",
      "requirement.unsupported.order_button.delivery.many": "Вызвать без $N$ пожеланий",
      ...
      // (далее предполагаемые значения ключей пишем в коментах)
  ],
 
  "order_button": {
    "__default__": {
      "one": "requirement.unsupported.order_button.one",
      "many": "requirement.unsupported.order_button.many",  // если нет some, то использовать many
    },
    "delivery": {
      "one": "requirement.unsupported.order_button.delivery.one",
      "many": "requirement.unsupported.order_button.delivery.many",  // если нет some, то использовать many
    },
    "courier": {
      "one": "requirement.unsupported.order_button.delivery.one",
      "many": "requirement.unsupported.order_button.delivery.many",  // если нет some, то использовать many
    }
  },
 
  "order_popup": {
    "__default__": {
        "popup_title": {
          "one": "requirement.unsupported.popup_title.one",                   // "Хотите уехать без $N$ пожелания?"
          "many": "requirement.unsupported.popup_title.many",              // "Хотите уехать без $N$ пожеланий?"
        },
        "popup_description": {
          "one": "requirement.unsupported.popup_description.one",  // "Этот тариф не поддерживает пожелание: $REQ"
          "many": "requirement.unsupported.popup_description.many",  // "Этот тариф не поддерживает пожеланиЯ: $REQ$"
        },
        "popup_order_button": {
          "one": "requirement.unsupported.popup_order_button.one",             // "Уехать без 1 пожелания"
          "many": "requirement.unsupported.popup_order_button.many",             // "Уехать без $N$ пожеланий"
        },
        "popup_alternative_button": {
          "one": "requirement.ski.unsupported.popup_alternative_button.one", // "Выбрать другой тариф"
          "many": "requirement.ski.unsupported.popup_alternative_button.many", // "Выбрать другой тариф"
        },
        // popup_description для неизвестного пожелания
        "popup_unknown_description" : {
          "one": "requirement.unknown.unsupported.popup_description.one",  // "Этот тариф не поддерживает выбранное пожелание"
          "many": "requirement.unknown.unsupported.popup_description.many",  // "Этот тариф не поддерживает выббранные пожеланиЯ"
        }
      },
   "delivery": {
      // здесь переписываем значения из __default__
      "popup_title": {
        "one": "requirement.unsupported.popup_title.delivery.one",                   // "Хотите вызвать без $N$ пожелания?"
        "many": "requirement.unsupported.popup_title.delivery.many",              // "Хотите вызвать без $N$ пожеланий?"
      },
      "popup_order_button": {
        "one": "requirement.unsupported.popup_order_button.delivery.one",             // "Вызвать без $N$ пожелания"
        "many": "requirement.unsupported.popup_order_button.delivery.many",             // "Вызвать без $N$ пожеланий"
      },
    }
  },
  
  // Категории, для которых отключить попап
  "disable_order_popup": ["courier", "cargo"],

  // Баббл для недоступного пожелания, если текст отсутствует в эксперименте
  "bubble_unavailable": "requirement.default.unsupported.bubble",          // "Сбросить недоступное пожелание"

  // 
  "multiclass": {
   "bubble_unavailable": "requirement.multiclass.unsupported.bubble",      // "Сбросить недоступные пожелания"
   "order_button": "requirement.multiclass.unsupported.order_button"       //  "Для заказа сбросьте пожелания"
  }

  "bubbles": {    
    // Простое требование
    "ski": {
      "icon_tag": "requirement.ski.icon_tag",                                // Тег картинки для отображения в бабле
      "bubble_available": "requirement.ski.bubble"                           // "Лыжи",
      "bubble_unavailable": "requirement.ski.unsupported.bubble",            // "Лыжи недоступны"
    },

    // multiselect требование
    "childchair": {
      "options": {
        "booster": {
          "icon_tag": "requirement.childchair.booster.icon_tag",                                // Тег картинки для отображения в бабле
          "bubble_available": "requirement.childchair.booster.bubble"                           // "Бустер",
          "bubble_unavailable": "requirement.childchair.booster.unsupported.bubble",            // "Бустер недоступен"
        },
        "infant": {
          "icon_tag": "requirement.childchair.infant.icon_tag",                                // Тег картинки для отображения в бабле
          "bubble_available": "requirement.childchair.infant.bubble"                           // "Люлька",
          "bubble_unavailable": "requirement.childchair.infant.unsupported.bubble",            // "Люлька недоступна"
        },
      }
    }
    ...
  }
```

#### Предзаказ и заказ другому
Отображаются на клиенте как требования, так что для них тоже подходит показывать баббл в случае недоступности, конфигурить можно так (`requirements_v2`):
```
{
  "l10n": [...],
  "bubbles": {
    // Обычные требования
    "__preorder__": {
      "bubble_unavailable": "requirement.preorder.unsupported.bubble", // Предзаказ недоступен
    },
    "__order_for_other__": {
      "bubble_unavailable": "requirement.order_for_other.unsupported.bubble", // Заказ другому недоступен
    }
}
```
_Если `bubble_available` не указан, значит при доступности требвания его не отображать_


#### Изменения в routestats API
В запрос `/routestats` клиент отправляет признак неоходимости использования нового флоу пожеланий.
```
"supported": [
    {
      "type": "requirements_v2"
    },
  ],
```
Это нужно для того, чтобы достоверно знать получил ли клиент эксперимент в ответе /zoneinfo. Рассинхронизация возникает в кейсе, когда на клиенте есть закэшированная зона, и происходит переключение эксперимента в админке.

По попаданию в эксперимент requirements_v2 не приходит `tariff_unavailable`/`unsupported_requirements` (они все равно не обрабатываются клиентами)
(если `"code": "unsupported_requirement")
* Цена и ETA в соседних категориях считаются без учета unsupported_requirements

#### Изменения в orderdraft API
В запрос `/orderdraft` клиент также отправляет флаг `requirements_v2`
```
"supported": [
    "requirements_v2"
  ],

В этом случае НП из requirements в оффере будут проигнорированы, как это работает для tariff_specific пожеланий.

#### Как делать на бекенде
В [протоколе](https://github.yandex-team.ru/taxi/backend-cpp/blob/822f7b18183b33dfd72d716db37c1e0006f5daba/protocol/lib/src/views/routestats/requirements.cpp#L41)
по эксперименту `requirements_v2` не считать категорию недоступной если в `/requirements` было НП
(практически вести себя так, в тч делать запросы в driver-eta и прайсинг как будто это требование tariff_specific)

#### Дальнейшие действия
удаление полей из эксперимента можно будет сделать после добавления их в zoneinfo API
(Расширять API сейчас не лучший момент, тк сервис переезжает и придется делать в 2х местах).
После проверки метрик и финализации структуры будет логично занести это внутрь dbtaxi.requirements и расширить админку требований чтобы управлять этим мог широкий круг людей.
