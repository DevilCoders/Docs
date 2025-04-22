
### Описание

Эксперимент superapp_screens описывает доступность сервисов супераппа (еда и лавка) на экранах выбора адреса и в поездке.

### Дальнейшее развитие 

Содержимое ответа эксперимента должно переехать в ответ ручки:

https://raw.github.yandex-team.ru/vadim-b/rfc/master/superapp/products.md

```
{
  "main": {
    "priority": [
      "eats",
      "grocery"
    ],
    "services": {
      "eats": {
        "enabled": true,
        "teasered": false,
        "show_splash": true,
        "show_disabled": false,
        "teasering_factor": 0.2,
        // переключает поведение дисмисса карточки супераппа
        // default иили отсутвие - означают старое поведение поведение (когда после скрола карточка дисмиссится сразу)
        // hide_or_bounce - новое поведение, когда перед скрытием будет работь bouncing
        "hide_strategy": "default" | "hide_or_bounce", // optional
        // Переключает поведение ресайза карточки супераппа при скролле или других событиях:
        // default или отсутствие - означает старое поведение (карточка имеет фиксированный размер и позицию, вне зависимости от скролла или других событий)
        // resize_along_scroll_axis - новое поведение: карточка меняет размер и позицию при скролле контента внутри нее:
        // - разворачивается на max размер при скролле контента в карточке вниз
        // - сворачивается в min размер при свайпе/скролле контента в карточке вверх
        "resize_strategy": "default" | "resize_along_scroll_axis" // optional
      },
      "grocery": {
        "enabled": true,
        "show_splash": true
      }
    }
  },
  "on_order": {
    "priority": [
      "eats",
      "grocery"
    ],
    "services": {
      "eats": {
        "enabled": false,
        "teasered": false
      },
      "grocery": {
        "enabled": true,
        "voice_file_url": "https://static.rostaxi.org/taximeter_welcome_sound/welcome_brand_eda_promo.ogg"
      }
    }
  }
}
```
