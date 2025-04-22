## Качество выделения аспектов из фото

### Процессы
* [Качество выделения из фото](https://reactor.yandex-team.ru/browse?selected=10200803) - расчет метрик качества
* [Аспект-фото](https://reactor.yandex-team.ru/browse?selected=10196537) - разметка в Толоке
* [дашборд](https://datalens.yandex-team.ru/s6f9g6vejqaul-aspekty?tab=Xp) - строится по kpi корзинам, для приемки метрик использовать аналогичные корзины без суффикса `_kpi`
---

### Как устроены метрики
см. `Качество выделения аспектов из текста` => `Как устроены метрики`
---

### YQL Запросы
| Запрос                          | Описание                                             |
|---------------------------------|------------------------------------------------------|
| `markup/prepare_pool.yql`       | подготовка пула для Толоки                           |
| `markup/process_result.yql`     | загрузка результатов разметки                        |
| `markup/update_final.yql`       | построение финальной таблицы из разметки             |
| `quality/precision_basket.yql`  | доливка данных в корзину точности выделения аспектов |
| `quality/precision_metrics.yql` | расчет точности выделения аспектов                   |
| `quality/recall_basket.yql`     | доливка данных в корзину полноты выделения аспектов  |
| `quality/recall_metrics.yql`    | расчет полноты выделения аспектов                    |
---

### Разметка `встречается ли аспект на фото`
* [Аспект-фото](https://reactor.yandex-team.ru/browse?selected=10196537)
* [шаблон](https://toloka.yandex.ru/requester/apps/vbLDabnAwRyf8PJRNM69) - в аккаунте `Я.Единорог`
* [качество разметки](https://datalens.yandex-team.ru/ticdas5kbityn-dashbordy-metrik-labsa-zakazchiki?state=4dffa784180)
* таблица с результатами разметки: `markup/aspect_image_final`
* как отправить данные на разметку:
    * в папке `markup/aspect_image_input` создать новую таблицу со схемой (`см. ниже`)
    * можно явно задать приоритет таблицы, навесив на нее числовой атрибут priority (50 - default, 90 - разметка для метрики)
    * можно явно сбросить кэш разметки через булевый атрибут skip_cache
    * таблицы отправляются на разметку в порядке уменьшения приоритета и возрастания даты создания, удаляются при попадании в пул
* при завершении разметки обновляется [артефакт](https://reactor.yandex-team.ru/browse?selected=10196865), в который записывается обработка какой таблицы закончена

Схема таблицы на вход графу разметки:
* `permalink: Int64`
* `namespace: String`
* `mds_group: Int64`
* `mds_name: String`
* `aspect_id: Int64`
---
---

## Выделение аспектов из фото

### Процессы
* [Построение данных для сниппетов](https://reactor.yandex-team.ru/browse?selected=10473930)
* [Обновление sprav_dict_layer.tar.gz](https://nirvana.yandex-team.ru/browse?selected=11852638) - сделано в рамках aspect_image, потому что здесь больше всего используется `SpravDict`
* [Прокачка фото](https://nirvana.yandex-team.ru/browse?selected=11857945) - прокачка фотографий товаров + прокачка выдачи по синонимам аспектов для набора эталонов
---

### Про модели от CV
[Общая вики](https://wiki.yandex-team.ru/computervision)

Есть основная модель (`sbr:1848907350`), у которой есть нужные для задачи аспектов выходы:
- `gpool_pool0` - основной слой (2048), поверх которого обучены все головы модели, использовать его, если много данных на каждый класс (есть модель, у которых этот слой выходной, а головы отрезаны: `sbr:1043266320`)
- `prod_v9_enc_i2t_v11_200_img` - эмбеддинг картинки, обученный на близость к тесту (есть в аватарнице и в кэше фоток Алтая `//home/altay/db/photo-unification/cache/mds` => `PhotoData.factors`)
- `prod_v10_enc_i2t_v12_200_img` - следующая версия эмбеддинга
- остальные головы описаны на вики

Модель для расчета эмбеддинга текста:
- [v11](https://a.yandex-team.ru/arc/commit/5550190) `prod_v9_enc_i2t_v11_200_txt`
    - https://yt.yandex-team.ru/hahn/navigation?filter=11&path=//home/geosearch/aspects/bin/text_embedding
- [v12](https://a.yandex-team.ru/arc/commit/7068158) `prod_v10_enc_i2t_v12_200_txt`
    - https://yt.yandex-team.ru/hahn/navigation?filter=12&path=//home/geosearch/aspects/bin/text_embedding
      [Инструмент для расчет эмбеддинга текста](https://a.yandex-team.ru/arc/trunk/arcadia/sprav/altay/photos/tools/text_embedding_calcer)
---

### Подбор порогов для синонимов аспектов
Для аспектов, у которых заполнены синонимы в поле `photo.image_embedding` подбирается порог для каждого синонима с целевой точностью с помощью UDF `AspectTools::ThresholdTuner`.
UDF работает в двух режимах (`aspect_image/threshold_tuning.yql`):
1. добавление результатов разметки к текущим синонимам + создание для синонимов новых итераций подбора параметров
2. сэмлпирование фото для синонимов в соответствие со значениями условий итерации

Данные по синонимам (поле `source_proto.photo.image_embedding.name` в Алтае) хранятся в таблице `aspect_image/phrase_info`
в формате `TPhraseInfo`, и по полю `TPhraseInfo::TStat` можно посчитать нужные пороги:
- порог для запуска в прод, например, с`precision >= 0.9`
- для разметки серой зоны для дообучения классификатора, например, с`0.2 <= precision < 0.8`
- в отдельную таблицу складываются синономы с плохим качеством, у которых ни для какого порога не достигается качество 0.9. Наличие синонима с хорошим качеством является необходимым условием, чтобы аспект попал в обучение

Для того, чтобы для синонима посчитались пороги, нужно:
- добавить его в поле `photo` в Алтае
- добавить в поле `aspect_statuses` значение "extracted_from_photos"

**Если в Алтае photo.image_embedding.threshold > 0, то будет значение из Алтая, а не подобранный порог**

#### Структуры данных
* `TPhraseInfo` - подбор порога для синонима (`Phrase`) аспекта
* `TPhraseInfo::TTuningIteration` - итерация подбора порога
* `TPhraseInfo::TImageInfo` - сэплированные фото для разметки
* `TPhraseInfo::TStat` - метрики для интервалов score
    * IntervalAccuracy - точность в пределах [MinScore, MaxScore)
    * IntervalAmount - кол-во примеров, на которых считается IntervalAccuracy
    * Precision - точность на интервале [MinScore, 1) с учетом распределения score на всех данных
    * Recall - полнота на интервале [MinScore, 1) с учетом распределения score на всех данных
---

### YQL UDF
* `AspectTools::BuildAvatarsUrl` - построение урла по `namespace`, `mds_group`, `mds_name` с учетом особенностей `namespace`
* `AspectTools::LabelDecoder` - декодирование предсказания модели в структурированные данные вида aspect_id, score
* `AspectTools::LabelEncoder` - кодирование множество исходных aspect_id в кортеж, в состав которого входят: в словарь с маппингом, сериализация в строку и кол-во классов
* `AspectTools::SimilarityCalcer` - расчет близости между эмбеддингом данной фотографии и набором эталонов для набора аспектов в разбивке по синонимам
* `AspectTools::ThresholdTuner` - инструмент подбора порогов для синонимов аспектов
---

### Обучение модели
Берется тело модели от CV и дообучается голова на таргет, где каждый элемент выхода - аспект

| Запрос                      | Описание                                        |
|-----------------------------|-------------------------------------------------|
| `train/sample_for_pool.yql` | сэмплирование данных для обучающего пула        |
| `train/prepare_pool.yql`    | расширение пула за счет искажения исходных фото |
| `train/join_embedding.yql`  | джоин эмбеддинга тела модели к фото корзины     |
| `train/apply.yql`           | применение обученной модели                     |
| `train/metrics.yql`         | расчет метрик                                   |

* [граф для обучения](https://nirvana.yandex-team.ru/flow/a4f4ba7f-e1ca-45a2-91e3-cec0f5cec002)
* [артефакт с продовой моделью](https://reactor.yandex-team.ru/browse?selected=10753262)
* [артефакт с тестовой моделью](https://reactor.yandex-team.ru/browse?selected=11258083)
---

### Полезные ссылки
* [головной таск](https://st.yandex-team.ru/WOA-1218)
* [данные на YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/geosearch/aspects/aspect_image)
