## Описание
Эксперимент superapp_parameters описывает конфигурационные параметры сервисов супераппа (Еда, Лавка, Аптеки) и без него невозможно пройти цикл заказа в сервисе.

### Тело эксперимента

```json
{
  "eats": {
    "url": "https://tc.mobile.yandex.net/4.0/eda-superapp/",
    "mode": "eats",
    "promo": "stories",
    "title": "superapp_eats_card_title",
    "enabled": true,
    "service": "eats",
    "support_chat_url": "https://m.taxi.yandex.ru/webview/chat/{lang}_int/eats",
    "service_name": "superapp_eats_service_name",
    "header_image_tag": "superapp_eats_header_tag",
    "splash_image_tag": "superapp_eats_splash_tag",
    "user_agent_component": "Superapp/Eats",
    "address_control_title": "superapp_eats_address_control_title",
    "shortcuts_service_name": "shortcuts_superapp_eats_service_name",
    "address_control_loading": "superapp_eats_address_control_loading",
    "address_input_placeholder": "superapp_eats_address_input_placeholder",
    "address_search_on_map_header": "superapp_eats_address_search_on_map_header",
    "courier_max_distance_to_focus": 5000
  },
  "grocery": {
    "url": "https://tc.mobile.yandex.net/4.0/eda-superapp/lavka",
    "mode": "grocery",
    "promo": "stories",
    "title": "superapp_grocery_card_title",
    "enabled": true,
    "service": "grocery",
    "support_chat_url": "https://m.taxi.yandex.ru/webview/chat/{lang}_int/eats",
    "subtitle": "superapp_grocery_card_subtitle",
    "service_name": "superapp_grocery_service_name",
    "header_image_tag": "superapp_grocery_header_tag",
    "splash_image_tag": "superapp_grocery_splash_tag",
    "user_agent_component": "Superapp/Grocery",
    "address_control_title": "superapp_grocery_address_control_title",
    "shortcuts_service_name": "shortcuts_superapp_grocery_service_name",
    "address_control_loading": "superapp_grocery_address_control_loading",
    "address_input_placeholder": "superapp_grocery_address_input_placeholder",
    "address_search_on_map_header": "superapp_grocery_address_search_on_map_header"
  },
  "tracking_api": "https://tc.mobile.yandex.net/4.0/eda-superapp/api/v2/orders/tracking",
  "l10n": [
    {
      "key": "superapp_eats_service_name",
      "tanker": {
        "key": "superapp.eats.service_name",
        "keyset": "client_messages"
      },
      "default": "Еда"
    },
    {
      "key": "superapp_eats_splash_tag",
      "tanker": {
        "key": "superapp.eats.splash",
        "keyset": "client_messages"
      },
      "default": "app_super_splash_eats_ru"
    },
    {
      "key": "superapp_grocery_splash_tag",
      "tanker": {
        "key": "superapp.grocery.splash",
        "keyset": "client_messages"
      },
      "default": "app_super_splash_grocery_ru"
    },
    {
      "key": "superapp_eats_header_tag",
      "tanker": {
        "key": "superapp.eats.header",
        "keyset": "client_messages"
      },
      "default": "app_super_header_eats_ru"
    },
    {
      "key": "superapp_grocery_header_tag",
      "tanker": {
        "key": "superapp.grocery.header",
        "keyset": "client_messages"
      },
      "default": "app_super_header_grocery_ru_taxi"
    },
    {
      "key": "superapp_eats_card_title",
      "tanker": {
        "key": "superapp.eats.card_title",
        "keyset": "client_messages"
      },
      "default": "Доставка из ресторанов"
    },
    {
      "key": "superapp_grocery_card_title",
      "tanker": {
        "key": "superapp.grocery.card_title_1",
        "keyset": "client_messages"
      },
      "default": ""
    },
    {
      "key": "superapp_grocery_card_subtitle",
      "tanker": {
        "key": "superapp.grocery.card_subtitle_1",
        "keyset": "client_messages"
      },
      "default": ""
    },
    {
      "key": "superapp_grocery_service_name",
      "tanker": {
        "key": "superapp.grocery.service_name",
        "keyset": "client_messages"
      },
      "default": "Продукты за 15 мин"
    },
    {
      "key": "superapp_eats_address_control_title",
      "tanker": {
        "key": "superapp.eats.address_control_title",
        "keyset": "client_messages"
      },
      "default": "адрес доставки"
    },
    {
      "key": "superapp_eats_address_control_loading",
      "tanker": {
        "key": "superapp.eats.address_control_loading",
        "keyset": "client_messages"
      },
      "default": "минутку…"
    },
    {
      "key": "superapp_eats_address_input_placeholder",
      "tanker": {
        "key": "superapp.eats.address_input_placeholder",
        "keyset": "client_messages"
      },
      "default": "Куда доставить?"
    },
    {
      "key": "shortcuts_superapp_grocery_service_name",
      "tanker": {
        "key": "shortcuts_superapp.grocery.service_name",
        "keyset": "client_messages"
      },
      "default": "Лавка"
    },
    {
      "key": "shortcuts_superapp_eats_service_name",
      "tanker": {
        "key": "shortcuts_superapp.eats.service_name",
        "keyset": "client_messages"
      },
      "default": "Еда"
    },
    {
      "key": "superapp_eats_address_search_on_map_header",
      "tanker": {
        "key": "superapp.eats.address_search_on_map_header",
        "keyset": "client_messages"
      },
      "default": "Адрес доставки"
    },
    {
      "key": "superapp_grocery_address_control_title",
      "tanker": {
        "key": "superapp.grocery.address_control_title",
        "keyset": "client_messages"
      },
      "default": "адрес доставки"
    },
    {
      "key": "superapp_grocery_address_control_loading",
      "tanker": {
        "key": "superapp.grocery.address_control_loading",
        "keyset": "client_messages"
      },
      "default": "минутку…"
    },
    {
      "key": "superapp_grocery_address_input_placeholder",
      "tanker": {
        "key": "superapp.grocery.address_input_placeholder",
        "keyset": "client_messages"
      },
      "default": "Куда доставить?"
    },
    {
      "key": "superapp_grocery_address_search_on_map_header",
      "tanker": {
        "key": "superapp.grocery.address_search_on_map_header",
        "keyset": "client_messages"
      },
      "default": "Адрес доставки"
    }
  ]
}
```

### Описание параметров

#### support_chat_url

Содержит ссылку на вебвью для открытия чата с саппортом. Ссылка должна шаблонизироваться относительно подстрок `{...}`. Параметры шаблонизации:
* `lang` — язык интерфейса клиента

**sic**: строка может не содержать шаблонных параметров.