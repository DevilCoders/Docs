## Конфиг парсера логов Метрики

### Структура конфига
Конфиг был разделен на две части. Они находятся в отдельной директории [statistics_config](https://a.yandex-team.ru/arc/trunk/arcadia/market/yamarec/yamarec/yamarec1/resources/statistics_config):
1. DJ плейсы  генерируются из [djid.json](https://a.yandex-team.ru/arc/trunk/arcadia/dj/services/market/libs/djid/config/djid.json)
2. Остальные плейсы находятся [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/market/yamarec/yamarec/yamarec1/resources/statistics_config/statistics.config) и подключаются в [итоговый](https://a.yandex-team.ru/arc/trunk/arcadia/market/yamarec/yamarec/yamarec1/resources/statistics_config/__root__) файл.

То есть, чтобы добавить новую программу DJ в парсер, нужно создать соответствующую запись в [djid.json](https://a.yandex-team.ru/arc/trunk/arcadia/dj/services/market/libs/djid/config/djid.json) и запустить скрипт обновления конфига (подробнее про это [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/dj/services/market/libs/djid/README.md#dobavlenie-novogo-djid)).

Чтобы поменять базовые параметры парсинга DJ-блоков (goal и теги), нужно изменить параметры subplace в файле [statistics.j2](https://a.yandex-team.ru/arc/trunk/arcadia/market/yamarec/tools/config_updater/template/statistics.j2) (например, за парсинг нетематических товарных блоков на главной странице Android отвечает сабплейс `_android_mainpage_product_block_subplace`).

Для не-DJ блоков конфиг [statistics.config](https://a.yandex-team.ru/arc/trunk/arcadia/market/yamarec/yamarec/yamarec1/resources/statistics_config/statistics.config) редактируется полностью вручную. 

В любом случае, **файл [\_\_root\_\_](https://a.yandex-team.ru/arc/trunk/arcadia/market/yamarec/yamarec/yamarec1/resources/statistics_config/__root__) вручную редактировать не надо** - он собирается из шаблона [statistics.j2](https://a.yandex-team.ru/arc/trunk/arcadia/market/yamarec/tools/config_updater/template/statistics.j2) запуском скрипта [update.sh](https://a.yandex-team.ru/arc/trunk/arcadia/market/yamarec/tools/config_updater/update.sh).



### Основные поля конфига
#### `goal_pattern`
регулярка на название события метрики.

---

#### `tag_pattern`
регулярка на тэги из гарсона события. 

Включает в себя поле id гарсона `garson["id"]` (всегда прописывается первым), а также тэги `garson["params"]["tag"]`. Id и разные тэги разделяются двоеточием `:`. Кроме того, в тэги записывается `cmsPageId` по каким-то историческим причинам, поэтому регулярки `tag_pattern` часто выглядят как-то так: `^(\d+:|)DJUniversalProducts$`. Здесь первая группа в скобках как раз отвечает за возможное наличие `cmsPageId` в событии.

---

#### `recommendation_type_pattern` 
регулярка на иные поля гарсона, отвечающие за разделение различных рекомендательных блоков. 

Список названий полей, к которым применяется это регулярное выражение, находится [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/market/yamarec/yamarec/yamarec1/udfs/statistics.py) в переменной `recommendation_type_keywords`. Если понадобится задать шаблон сразу для нескольких полей из этого списка, следует прописать значения полей в том же порядке, в котором идут названия полей в списке, разделяя двоеточием `:`. В случае разделителя dj_meta_place в событии обычно присутствует и dj_place, поэтому, если нужен фильтр только на dj_meta_place (с любым dj_place), стоит писать регулярку вида `^metaplace(:[\w:]*|)$`.


Если появляется новое поле, выполняющее роль разделителя блоков в гарсоне, следует дописать название этого поля в список `recommendation_type_keywords`, а регулярки для этого поля записывать в `recommendation_type_pattern`.

---

#### `records`
список настроек для юнит-тестов.

Юнит-тесты, по сути, генерируют события, подставляя название ключей из регулярок в шаблон, а потом проверяют, что все события распарсились. 

Каждый элемент `records` - кортеж, задающий одно тестовое событие. Состоит из следующих позиций:
- указание платформы (например, `"hit_desktop"`). Влияет на то, какой хост будет у тестового события. При добавлении новых событий можно просто копипастить это поле из событий той же платформы.
- тип объекта, который описывает событие (прокидывается в таблицы yamarec). На данный момент актуальные типы - `"model"` для товарных блоков (если событие метрики содержит `productId`) и `"navnode"` для категорийных блоков (если событие метрики содержит что-то из {`navnodeId`, `categoryId`, `hid`, `nid`}). Для поддержки новых типов, возможно, нужно будет дописывать их в код парсера.
- номер шаблона (например, `56`). Шаблоны находятся в [этом файле](https://a.yandex-team.ru/arc/trunk/arcadia/market/yamarec/yamarec/tests/unit/parse_metrika/templates.py). Они представляют собой набор ключей события (необязательно полный), заполненый `null`-ами. Шаблоны должны содержать необходимый минимум ключей события, которые используются для парсинга (то есть ключей, значения которых позволяют идентифицировать блок). Если новый блок похож на какой-то из уже существующих (например, на морду добавляется скроллбокс с новой программой DJ) - скорее всего, можно взять номер шаблона из конфига для парсинга существующего блока, проверив, что в нем действительно есть все нужные поля. Если для нового блока на фронте заново создавались события метрики - скорее всего, нужно добавить новый шаблон в указанный файл.  
- (опционально) название цели для тестового события (например, `"CMS-PAGE_SCROLLBOX_SNIPPET_NAVIGATE"`). Если не указано, будет использоваться самое длинное название цели из `goal_pattern`. Лучше указывать явно, потому что нередко со временем у блока меняются цели, что отражается в конфиге.
- (опционально) тег тестового события (например, `"DJ"`). Если не указан, будет использоваться самый длинный тег из `tag_pattern`. Имеет смысл указывать, если в `tag_pattern` перечислено больше одного шаблона через `|`.

### Про тесты

Общая информация про тесты yamarec [тут](https://a.yandex-team.ru/arc/trunk/arcadia/market/yamarec/yamarec/README.md#testy).
Юнит-тесты запускаются командой `./ya m -A market/yamarec/yamarec/tests/unit` из корня Аркадии или автоматически в интерфейсе Arcanum при коммите. 

Помимо юнит-тестов, есть еще так называемые `stubs` на задачу. В них содержатся заданные вручную события метрики для [веба](https://a.yandex-team.ru/arc/trunk/arcadia/market/yamarec/yamarec/yamarec1/resources/templates/stubs/logfeller_bs_watch_log_1d.0.json.j2) и [приложения](https://a.yandex-team.ru/arc/trunk/arcadia/market/yamarec/yamarec/yamarec1/resources/templates/stubs/logfeller_metrika_mobile_log_1d.0.json.j2), а также [ожидаемый результат парсинга](https://a.yandex-team.ru/arc/trunk/arcadia/market/yamarec/yamarec/yamarec1/resources/templates/stubs/events_metrika_actions.0.json.j2). 

Стабы проверяют парсинг конкретного указанного события, и кроме самого факта парсинга события проверяют еще и то, какие данные попадут в context в табличках yamarec. Поэтому стабы стоит добавлять, исходя из здравого смысла - если уже есть шаблон для события с тем же набором параметров (пусть и другой целью), то можно не добавлять.

Задача, достающая клики и показы из логов метрики, называется `GetActionsFromMetrika`. Локально тесты на задачу проще всего запустить через [демона](https://a.yandex-team.ru/arc/trunk/arcadia/market/yamarec/yamarec/README.md#zapusk-demona).

## Прокидывание параметров из событий фронта в context событий yamarec
За это отвечают два списка в файле [statistics.py](https://a.yandex-team.ru/arc/trunk/arcadia/market/yamarec/yamarec/yamarec1/udfs/statistics.py). 

Сначала нужно достать параметр из события в коде парсера. 

Если нужное поле находится в гарсоне или в корне события метрики, то все просто - список названий полей, которые нужно достать, задается в переменной `keywords_to_context`. После этого в парсере `_parse_metrika_params` поля преобразуются из camelCase в snake_case (это сделано потому, что на вебе и в приложениях отличаются стили нейминга параметров, а в yamarec хотим иметь единый стиль и единое название поля для всех платформ) и кладутся в `entity`.

Если поле находится в каком-то более экзотическом месте события (например, внутри словаря), или нужно делать какие-то преобразования, кроме конвертирования в строку, то придется отдельно обрабатывать случай в коде парсера и класть поле в `entity`.  

Затем, чтобы поле попало из `entity` в `context` события, надо прописать его название (в snake_case) в список `additional_context_keys`.  В качестве примера - поле `parent_promo_id` (а `parentPromoId` прописано в `keywords_to_context`).


## Добавление блоков на дашборды 

Дашборды [тут](https://datalens.yandex-team.ru/a8tmqi48dj4k6-marketrecom?tab=pKP)

[JS-файл с конфигом дашбордов](https://datalens.yandex-team.ru/editor/1peooglqlddc0-chart-descriptions)


#### Морда
В простейшем случае нужно добавить строчку с плейсом блока в [js-файл](https://datalens.yandex-team.ru/editor/1peooglqlddc0-chart-descriptions) для нужной платформы: 
Списки блоков для четырех платформ начинаются со строчки ~2563 (искать первое вхождение `MainPageDesktop_common_places`, ниже остальные платформы). После этого блок должен появиться на всех графиках вкладки **"Морда"**.

#### Карточка модели
С блоками на **карточке модели** чуть посложнее. Они находятся в нижней части [js-файла](https://datalens.yandex-team.ru/editor/1peooglqlddc0-chart-descriptions) (искать функцию `make_block_platform_graphs`). Если блок имеет одинаковые суффиксы (часть после названия платформы) на всех платформах, достаточно прописать вызов функции с этим префиксом, например `make_block_platform_graphs('ModelCardAlsoViewed');`. Если суффиксы отличаются, нужно задать плейсы для каждой платформы вручную:
```
// Карточка модели - Совместно покупаемые товары
complementary_desktop_places = ['ModelCardComplementaryItems', 'DesktopModelCardComplementaryItems'];
complementary_touch_places = ['TouchModelCardComplementaryItems'];
complementary_ios_places = ['BlueIOSModelCardComplementary', 'IOSModelCardComplementary'];
complementary_android_places = ['BlueAndroidModelCardComplementary', 'AndroidModelCardComplementary'];
make_block_platform_graphs_by_places('ModelCardComplementary', complementary_desktop_places, complementary_touch_places, complementary_ios_places, complementary_android_places);
```
