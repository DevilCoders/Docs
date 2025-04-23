## Доработка VisibilityHelper для удобства добавления приложений

### Как сейчас

Сейчас VisibilityHelper получают с помощью метода GetVisibilityHelperBySource,
в который передается `models::requestsource::Source` --
enum для разделения поведения приложений Яндекс.Такси и Убера.
Далее на основе значения enum'а производится манипуляция с наборами категорий
для разных приложений, которые берутся из конфигов, например:
```c++
classes_config.all_categories - classes_config.uber_categories
classes_config.all_categories & classes_config.uber_categories
```
Получается, что при добавлении новых приложений нужно заводить новые конфиги и
дописывать код для манипулиций наборами категорий.

Такое решение не очень гибкое и затрудняет добавление новых приложений.

### Что предлагается

Инициализировать VisibilityHelper на основе значения `ClientApp.name` --
полного имени приложения. Для этого нужно два новых конфига.

#### Конфиг `APPLICATION_MAP_BRAND`

Мэппинг из полного имени приложения в shortname приложения (brand),
для которого будет задаваться набор категорий. В будущем,
если shortname приложения будет парситься в структуру `ClientApp`,
от этого конфига можно будет отказаться за ненадобностью.

```json
{
  "__default__": "yataxi",
  "mobileweb_uber": "yauber",
  "mobileweb_uber_android": "yauber",
  "mobileweb_uber_az_android": "yauber",
  "mobileweb_uber_az_iphone": "yauber",
  "mobileweb_uber_by_android": "yauber",
  "mobileweb_uber_by_iphone": "yauber",
  "mobileweb_uber_iphone": "yauber",
  "mobileweb_uber_kz_android": "yauber",
  "mobileweb_uber_kz_iphone": "yauber",
  "mobileweb_yango": "yango",
  "mobileweb_yango_android": "yango",
  "mobileweb_yango_iphone": "yango",
  "uber_android": "yauber",
  "uber_az_android": "yauber",
  "uber_az_iphone": "yauber",
  "uber_by_android": "yauber",
  "uber_by_iphone": "yauber",
  "uber_iphone": "yauber",
  "uber_kz_android": "yauber",
  "uber_kz_iphone": "yauber",
  "web_uber": "yauber",
  "web_yango": "yango",
  "yango_android": "yango",
  "yango_iphone": "yango"
}
```

#### Конфиг `APPLICATION_BRAND_CATEGORIES_SETS`

Мэппинг из shortname приложения (brand) в набор категорий,
которые соответствуют приложению.

```json
{
  "__default__": [
    "express",
    "econom",
    "business",
    "comfortplus",
    "vip",
    "pool",
    "ultimate",
    "maybach",
    "minivan",
    "business2",
    "drivers_pool",
    "child_tariff",
    "start",
    "standart",
    "mkk",
    "selfdriving",
    "demostand",
    "promo",
    "premium_van",
    "mkk_antifraud",
    "cargo",
    "personal_driver",
    "suv",
    "premium_suv",
    "universal",
    "night"
  ],
  "yauber": [
    "uberx",
    "uberselect",
    "uberblack",
    "uberkids",
    "uberstart",
    "uberlux",
    "ubervan",
    "uberselectplus",
    "ubernight"
  ],
  "yango": [...]
}
```

Таким образом, отвязываемся от логики `yataxi_categories = all_categories - yauber_categories`,
для каждого приложения будет явно задан список категорий.
Ключ `__default__` по сути описывает `yataxi`, явно `yataxi` не задаем
для избежания дублирования списка категорий. Конфиг `ALL_CATEGORIES`
будет использоваться в качестве достоверного источника полного списка категорий.
