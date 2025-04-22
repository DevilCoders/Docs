# DistributionLoader - загрузчик виджетов дистрибуции

**Зачем?**
Данный лоадер определяет по месту его расположения, какую cms страницу с виджетами дистрибуции необходимо загрузить.
Страница содержит набор виджетов дистрибуции различной конфигурации для различных акций, которые могут скрываться по некоторым ограничениям.

# Данные

Страница спасибо за заказ не cms'сизированна и нет возможности вставить виджет AppDistributionBanner через cms.
Но в планах есть задача на перевод страницы на cms. Времено делаем Loader который будет грузить специальную разметку cms для баннера.

## AppDistributionBanner - виджет баннер с дистрибуцией мобильного приложения

### Ограничения на cms страницу
+ Страница должна содержать одну строку
+ Строка страницы должна содержать одну колонку

**Важно:** Если ограничения не будут выполнены, например страница будет содержать больше одной строки или больше одной колонки, то в коде будут учитываться только первые элементы. Если после фильтрации виджетов, по условиям, имеется больше одного виджета для отображения, то будет взят первый виджет по порядку.

### Алгоритм добавления нового использования виджета дистрибуции
+ Если добавляется новый виджет дистрибуции, то его необходимо добавить в mapping (_src/widgets/parts/AppDistribution/DistributionLoader/mapping.js_)
+ Расширить маппинг места отображение и типа cms страницы
    - Добавить новое место расположение в `SHOW_PLACE` (_src/widgets/parts/AppDistribution/DistributionLoader/types.js_)
    - Добавить новый тип cms страницы в `CMS_PAGE` (_src/entities/cms_)
    - Расширить `WIDGET_TYPE_BY_SHOW_PLACE` (_src/widgets/parts/AppDistribution/DistributionLoader/helpers.js_)
+ В редакторе схемы cms создать новый тип узла контента со следующими параметрами
    - **Свойства типа**
        - _export_include_content_ = ROWS
        - _export_include_full_ = ROWS
        - _label_ - Содержит описательное наименование узла
    - **Свойства полей**
        - _ROWS_
            - _allowedTypes_ = ROW_REACT_24
            - _allowedValuesMin_ = 0
            - _allowedValuesMax_ = 200
    - **Шаблоны экспорта**
        - Первый шаблон
            - _Шаблон_

                    {
                        "rows": [__ROWS__]
                    }

            - _Формат экспорта_ = phone.json
        - Второй шаблон
            - _Шаблон_

                    {
                        "rows": [__ROWS__]
                    }

            - _Формат экспорта_ = desktop.json
+ В редакторе схемы cms создать новый тип корневого узла
    - **Свойства типа**
        - _export_include_content_ = TYPE, CONTENT, ID
        - json_skip_null_fields = true
        - _label_ - Содержит описательное наименование узла
    - **Свойства полей**
        - _CONTENT_
            - _allowedTypes_ = тип узла контента созданного на предыдущем шаге
            - _allowedValuesMin_ = 1
            - _allowedValuesMax_ = 1
            - _disabled_ = true
            - _ui_collection_ = content
            - _label_ - Содержимое
        - _TYPE_
            - _hidden_ = true
            - _export_name_ = type
            - _allowedValuesMin_ = 1
            - _allowedValuesMax_ = 1
            - default_value = {{type}}
        - _LINKS_
            - _allowedTypes_ = PAGE_LINKS
            - _allowedValuesMin_ = 1
            - _allowedValuesMax_ = 1
            - default_value = PAGE_LINKS
            - _label_ = Связи
            - _ui_collection_ = bindings
        - _ID_
            - _value_type_ = number
            - _hidden_ = true
            - _allowedValuesMin_ = 0
            - _allowedValuesMax_ = 1
            - default_value = {{docId}}
    - **Шаблоны экспорта**
        - Первый шаблон
            - _Шаблон_

                    {
                        "content": __CONTENT__,
                        "type": __TYPE__,
                        "links": __LINKS__,
                        "id": __ID__
                    }

            - _Формат экспорта_ = desktop.json
+ В редакторе схемы cms создать новый тип материала
    - **Свойства материала**
        - _Заголовок_ = Содержит описательное наименование
        - _Корневой узел_ = Узел созданный на предыдущем шаге
    - **Форматы экспорта**
        - _desktop.json.full_
            - _URL_ = /
            - _Шаблоны ключей_ = device, domain, ds, format, type, zoom
        - _phone.json.full_
            - _URL_ = /
            - _Шаблоны ключей_ = device, domain, ds, format, type, zoom
+ В cms создать новый материал на основе созданных типов
    - Добавить одну строку
        **Важно** Если нужно что бы отображался на всю ширину страницы необходимо в `Визуальных свойствах` строки задать свойство `Ширину` со значением `По ширине контейнера`
    - Добавить один столбец
    - Добавить виджеты дистрибуции