# Matcher
Набор инструментов для матчинга детекций знаков. Предполагается pipeline из этапов:
1. Маскирование картинки
2. Детектирование объектов
3. Независимое выделение дескрипторов
4. Отбор пар картинок, как кандидатов для матчинга
5. Матчинг детекций
6. Кластеризация детекций

Выходом каждого этапа является таблица с фиксированной схемой, чтобы реализацию этапов можно было варьировать.

# Датасеты
Доступные датасеты можно найти [здесь](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/mrc/signs_map).

# Сборка

`ya make -r -DTENSORFLOW_WITH_CUDA=1 -DCUDA_VERSION=10.1 -DNO_DEBUGINFO`


# Шаг I (маскирование)
Сначала для картинок вычисляется маска ([height x width] матрица mask), которая определяет для каких пикселей стоит вычислять дескрипторы:
- mask[i, j] = 0 - отброшенный пиксель
- mask[i, j] > 0 - полезный пиксель
Запуск организуется, как map-операция на YT.
Пример запуска генерации дескрипторов можно найти ниже.
Для запуска на видеокарте есть параметр ```--gpu```.

```
mask.py
    --feature-table //tmp/feature  # input feature table \
    --feature-mask-table //tmp/feature_mask # output table \
    --gpu gpu_geforce_1080ti # use 1080 ti \
```

В качестве выхода будет получена таблица feature расширенная полем ```mask_png_base64```, это строка с маской которая, сохранена, как png картинка в формате base64.

# Шаг II (детектирование знаков)
Знаки описываются тремя параметрами:
    1. object_id - id объекта, должен быть уникален на одном изображении
    2. bbox - координаты знака на изображении (в координатах изображения из mds)
    3. type - тип знака
Запуск организуется, как map-операция на YT.
Пример запуска детектирования объектов можно найти ниже.
Для запуска на видеокарте есть параметр ```--gpu```.

```
detector.py
    --feature-mask-table //tmp/feature  # input feature mask table \
    --features-objects-yt-json //tmp/features_objects # output json in YT \
    --gpu gpu_geforce_1080ti # use 1080 ti \
```

В качестве выхода будет получена таблица с тремя столбцами:
    1. feature_id - id фотографии
    2. orientation - ориентация фотографии
    3. objects - список объектов на фотографии

### Шаг III (фильтрация пар кандидатов)
Следующим шагом происходит фильтрация пар изображений, на которых мы ожидаем увидеть матчи детекций.
Если два изображения достаточно близки и смотрят в одном направлении, а так же на них найдены одинаковые типы знаков, то эта пара попадает в список кандидатов.
Минимальный размер детекций, которая будет рассматриваться, регулируется с помощью параметра ```--min-box-size```. Пример запуска с разбором ниже.

```
filter_match_candidates.py \
    --feature-table //tmp/feature # input feature table \
    --object-file //tmp/object.json # yt json file with detections \
    --distance 60 # maximum distance between features in meters \
    --heading-diff 90 # max feature heading diff in degrees \
    --min-box-size 30 # optional, max box size > threshold \
    --pair-table //tmp/pair # output table \
```

В качестве выхода будет получена таблица их двух колонок *first* и *second*, где каждая хранит полное описание feature.


## Шаг IV (дескрипторы и поиск соответствий)
На этом этапу для полученного списка пар кандидатов производится матчинг детекций.
Вычисления идут снова на YT в виде map-операции, каждая пара рассматривается независимо.

Матчинг производится на основе дескрипторов.
Для того, чтобы добавить новый тип дескриптора, необходимо определить свой метод и добавить его в список ```options``` в файле *descriptor_algorithm.py*.
На вход подается:
- image – **BGR** изображение (земля внизу) в виде numpy матрицы
- mask – маска виде numpy матрицы, которая определяет для каких пикселей вычислять дескприпторы:
  - mask[i, j] = 0 - отброшенный пиксель
  - mask[i, j] > 0 - полезный пиксель

Возвращается кортеж:
- points – Nx2 матрица особых точек (float32).
- descriptors – NxD матрица дескрипторов (построчно, float32)
- confidence – N вектор увереностей (float32)

Ниже приведен пример для **sift** детекторов.
```
def sift(image, mask):
    detector = cv.SIFT_create(2000)
    gray = cv.cvtColor(image, cv.COLOR_BGR2GRAY)
    key_points, descriptors = detector.detectAndCompute(gray, mask)

    return (
        np.float32(list(map(lambda kp: kp.pt, key_points))),
        np.float32(descriptors),
        np.ones((size, ), dtype=np.float32)
    )
```

Затем в той же самой операции производится матчинг на основе полученных дескрипторов.
Функция матчинга принимает для каждой из картинок MatchContext:
- feature: Feature
- points: Nx2 numpy array[float32]
- descriptors: NxD numpy array[float32]
- confidence: N numpy array[float32]
- detections: list[Detection]

Класс ```Detection``` хранится в *detection.py* и имеет структуру:
- id: int
- type: str
- box: Box

Можно добавить свою реализацию и добавить её в список ```options``` в файле *match_algorithm.py*.
На вход принимает два контекста, а на выходе ожидается список троек (first_detection_id, second_detection_id, confidence).
Детекции в получаемых контестах уже повернуты в соответствии со значением orientation.

Схематичный пример реализации матчинга ниже:

```
def knn_match(first, second)
    mathes = match(first.descriptors, second.descriptors)

    F = find_fundamental(first.points, second.points, matches)
    if F is None:
        return []

    pairs = []
    for detection in first.detections:
        for other in second.detections:
            if is_match(detection, other, F):
                pairs.append((detection.id, other.id, 1.0))
```

Пример запуска матчинга можно найти ниже. Для запуска на видеокарте есть параметр ```--gpu```.

```
match.py \
    --pair-file pair.json # input feature pairs' file \
    --mask-table //tmp/sift # input mask table \
    --object-file //tmp/object.json # yt json file with detections \
    --match-table //tmp/match # output table \
    --gpu none # optional, don't use gpu now \
    --descriptor-type sift $ descriptor algorithm type
    --match_type knn_match # match algorithm type
```

В качестве выхода будет получена таблица следующего формата:
- feature_id_1: int
- feature_id_1: int
- matches: list
  - object_id_1: int
  - object_id_2: int
  - confidence: float

Можно получить результаты с матчами из таблицы в принятом у нас [формате](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/eye/experiments/signs_map/readme.md), чтобы замерить качество.

```
export.py \
    --match-table //tmp/match # table to export \
    --out-file match.json # output json file with matches \
```

### Шаг V (кластеризация)
Следующим этапом мы получаем кластеры из имеющихся матчей. Работа происходит локально,
на вход принимается json файл с матчами, а на выход с кластерами (формат можно найти [тут](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/eye/experiments/signs_map/readme.md)).

```
./cluster.py \
    --match-file match.json # input json file with matches \
    --cluster-file cluster.json # output json file with cllusters \
    --type greedy \
    --min-box-size 30 \
    --min-confidence 0.001 \
    --object-file //tmp/object.json
```

Для удобства работы вводится пара ```feature_object_id = (feature_id, object_id)```.
Функция кластеризации принимает список матчей ```(feature_object_id_1, feature_object_id_2, confidence)```
и список детекций (список всех feature_object_id), а также минимальный порог для ребра.

Можно добавить свою реализацию и добавить её в список ```options``` в файле *cluster.py*.
