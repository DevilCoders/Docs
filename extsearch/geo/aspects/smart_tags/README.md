### Процессы
* [Построение смарт тегов](https://reactor.yandex-team.ru/browse?selected=10053158) - построение смарт тегов, расчет метрик качества, отправка данных на разметку для метрик и обучающего пула
* [Аспект-компания](https://reactor.yandex-team.ru/browse?selected=9799811) - разметка в Янге
* [дашборд](https://datalens.yandex-team.ru/s6f9g6vejqaul-aspekty?tab=Xp)
---

### Подготовка данных
| Запрос                                | Описание                                |
|---------------------------------------|-----------------------------------------|
| `company_data/2gis_tags.yql`          | признаки компаний в 2ГИС                |
| `company_data/companies.yql`          | парсинг snapshot/company                |
| `company_data/prices.yql`             | прайсы организаций                      |
| `company_data/reviews.yql`            | отзывы организаций + выделенные аспекты |
| `company_data/social_urls_filter.yql` | тексты из соц. сетей организаций        |
| `company_data/url_content_attrs.yql`  | тексты всех урлов организаций           |
| `company_data/zoon.yql`               | признаки компаний в Zoon                |
---

### Структуры данных
* TFeatureCalculatorInput
* TFeatureCalculatorOutput
* TCompanyData + TReview, TUrl, TPriceItem, TPhoto
* TMarkupItem
* TPoolBuilderInput
* TPoolItem
* TFormattedPoolItem
* TYangTemplateAssessment
---

### YQL Запросы
| Запрос                          | Описание                                             |
|---------------------------------|------------------------------------------------------|
| `train/feature_calculation.yql` | расчет признаков                                     |
| `train/pool.yql`                | построение пула для обучения                         |
| `train/format_pool.yql`         | форматирование пула для катбуста                     |
| `train/cd.yql`                  | column description для катбуста                      |
| `train/apply.yql`               | применение модели к данных из `feature_calculation`  |
| `train/metrics.yql`             | расчет метрик качества модели                        |
| `train/pool_markup.yql`         | данные для разметки для обучающего пула              |
| `prepare.yql`                   | построение смарт тегов                               |
| `quality/basket.yql`            | расчет корзины для смарт тегов по по свежей разметке |
| `quality/basket_markup.yql`     | данные для разметки для метрик качества              |
| `quality/metrics.yql`           | расчет метрик качество сниппетов смарт тегов         |
---

### YQL UDF
* `AspectTools::GazetteerAspectExtractor` - выделение аспектов из текста газетиром, костыль для работы списков лучшего
* `AspectTools::YangTemplateConveter` - конвертация атрибутов компании и списка аспектов в формат для шаблона разметки аспект-компания
* `AspectTools::FeatureCalculator` - расчет признаков
* `AspectTools::FeatureNames` - названия признаков
* `AspectTools::PoolBuilder` - сбор пула для обучения + сплит
* `AspectTools::PoolFormatter` - форматирование пула в формат Catboost
---

### Разметка `есть ли аспект у компании`
* [Аспект-компания](https://reactor.yandex-team.ru/browse?selected=9799811)
* [шаблон](https://yang.yandex-team.ru/requester/project/11518) - в аккаунте `Янг.Справочник`
* [инструкция](https://wiki.yandex-team.ru/eva/sprav/instrukcija-dlja-ocenki-atributa-kuxnja)
* [качество разметки](https://datalens.yandex-team.ru/p0ex96615mi8i-aspekty-obshepita)
* таблица с результатами разметки: `markup/aspect_company_final`
* как отправить данные на разметку:
    * в папке `markup/smart_tags_input` создать новую таблицу со схемой (`см. ниже`)
    * можно явно задать приоритет таблицы, навесив на нее числовой атрибут priority (50 - default, 90 - разметка для метрики)
    * можно явно сбросить кэш разметки через булевый атрибут skip_cache
    * таблицы отправляются на разметку в порядке уменьшения приоритета и возрастания даты создания, удаляются при попадании в пул

Схема таблицы на вход графу разметки:
* `permalink: Int64`
* `aspect_id: Int64`

| Запрос                      | Описание                                 |
|-----------------------------|------------------------------------------|
| `markup/prepare_pool.yql`   | подготовка пула для Толоки               |
| `markup/process_result.yql` | загрузка результатов разметки            |
| `markup/update_final.yql`   | построение финальной таблицы из разметки |
---

### Модель аспект-компания
Модель должна предсказывать по разметке факт наличия данного аспекта в организации используя доступную информацию из ее атрибутов, отзывов, фото. При использовании в проде налагается дополнительное условие на сортировку (чтобы выше ранжировались те аспекты, которые более специфичны для данной организации).
* [шаблонный граф для обучения модели](https://nirvana.yandex-team.ru/flow/84dda7a1-de06-4946-aa25-fce2aa3860f2)
* [артефакт с актуальной моделью](https://reactor.yandex-team.ru/browse?selected=10050322)

---

### Полезные ссылки
* [головной таск](https://st.yandex-team.ru/WOA-1325)
* [данные на YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/geosearch/aspects/smart_tags)
