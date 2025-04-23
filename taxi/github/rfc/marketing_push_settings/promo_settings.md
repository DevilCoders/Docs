## Промоутирование настроек

Тикет: https://st.yandex-team.ru/TAXIMOBILEDEV-361 Нотификация-оповещение о выключенных уведомлениях

Макет:
![push_settings](https://jing.yandex-team.ru/files/muhrynov/Screenshot%20at%20Nov%2027%2012-21-53.png)

### Реализация

В v1/products добавляется кэшируемый эксперимент promo_marketing_push_settings &mdash; 
он хранит структуру и параметры отображения оповещений клиентов:
- `push_disabled_popup` &mdash; оповещение о выключенных в системных настройках пушах,
  показывается, если у клиента отключены пуши в системных настройках;
- `push_settings_popup` &mdash; оповещение о возможности настроить пуши внутри приложения,
  показывается после того, как клиент смахнул какой-нибудь рекламный пуш не посмотрев
  (эта логика ещё обсуждается и будет уточняться, решение не финальное).

Для оповещений возвращаются значения `title`, `subtitle`, `image_tag` (для иконки слева) и 
параметры отображения в объекте `show_policy`:
- `enabled` &mdash; включен ли показ данного оповещения;
- `max_show_count` &mdash; задаёт максимальное число показа оповещения пользователю
  (если параметр не задан, то число показов не ограничено);
- `show_interval_days` &mdash; задаёт минимальный интервал (в днях) между
  последовательными показами оповещения польвателю.

#### Пример ответа `/4.0/mlutp/v1/products` с promo_marketing_push_settings
```json5
{
    ...
    "typed_experiments": {
        "items": [
            ...
            {
                "name": "promo_marketing_push_settings",
                "value": {
                    "l10n": {
                        "push_disabled_popup.title": "Включите уведомления",
                        "push_disabled_popup.subtitle": "Так вы сможете следить за статусами ваших заказов ",
                        "push_settings_popup.title": "Настройка уведомлений",
                        "push_settings_popup.subtitle": "Вы можете управлять тем, какие уведомления хотите получать"
                    },
                    "push_disabled_popup": {
                        "image_tag": "icon_image_tag",
                        "show_policy": {
                            "enabled": true,
                            "max_show_count": 3,
                            "show_interval_days": 7
                        },
                        "subtitle": "push_disabled_popup.subtitle",
                        "title": "push_disabled_popup.title"
                    },
                    "push_settings_popup": {
                        "image_tag": "icon_image_tag",
                        "show_policy": {
                            "enabled": true,
                            "max_show_count": 3,
                            "show_interval_days": 7
                        },
                        "subtitle": "push_settings_popup.subtitle",
                        "title": "push_settings_popup.title"
                    }
                },
                "cache_status": "no_cache"
            }
        ],
    }
}
```

#### Схема эксперимента promo_marketing_push_settings
```yaml
type: object
required:
  - push_disabled_popup
  - push_settings_popup
  - l10n
properties:
  push_disabled_popup:
    $ref: "#/definitions/PopUp"
  push_settings_popup:
    $ref: "#/definitions/PopUp"
  l10n:
    $ref: "l10n.yaml#/l10n"
additionalProperties: false

definitions:
  ShowPolicy:
    type: object
    additionalProperties: false
    required:
      - enabled
    properties:
      enabled:
        type: boolean
      max_show_count:
        type: integer
      show_interval_days:
        type: integer
  
  PopUp:
    type: object
    additionalProperties: false
    required:
      - title
      - subtitle
      - image_tag
      - show_policy
    properties:
      title:
        type: string
      subtitle:
        type: string
      image_tag:
        type: string
      show_policy:
        $ref: "#/definitions/ShowPolicy"
```
