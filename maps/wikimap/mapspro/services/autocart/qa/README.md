# Проверка метрики оценки качества контуров зданий

Цель:
- экспериментально оценить точность метрики
- повторить процедуру обучения модели


## Комплект поставки метрики

1. Описание алгоритма и инструкции по применению тулов
2. Стенд для разметки контуров
3. Тул для оценки качества контуров

### Стенд для разметки контуров
Исходный код стенда находится тут: https://github.com/KruchDmitriy/ymap-auto-markup/tree/master/labeler-app

Исходный код стенда с небольшими правками перенесен в репозиторий Arcadia: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/autocart/qa/labeler_app

Поднятие окружения:
```
python3 -m virtualenv .env
source .env/bin/activate
pip install -r requirements.txt
```

`generate_task.py` -- тул для генерации заданий для разметки
опции
* `--data` -- путь до shape-файла с контурами в проекции EPSG:4326,
    у каждого объекта должны быть определены атрибуты id, transform
* `--out_dir` -- директория для сгенерированных заданий (./data/markup_tasks )
* `--task_size` -- количество контуров в одном задании
* `-n` -- количество заданий

Для запуска стенда нужно выполнить:
```
uwsgi --http-socket 0.0.0.0:5000 --plugin python34 -w server:app -H .env
```
В результате веб-интерфейс стенда будет доступен по 5000-му порту.

Генерирует файлы `data/markup_tasks/taskN.json`, содержащий список объектов вида
```json
[
    {"coords": [[lon1, lat1], [lon2, lat2], ...[lonn, latn]],
    "id": "117",
    "meta": {"transform": null}
    },
    ...
]
```

Стенд вычитывает задания из `./data/markup_tasks`, а результаты разметок дописывает в файл `./data/results.json`
Файл `results.json` содержит список объектов вида
```json
[
    { "results":
        [
            {
                "isBad": false,
                "id": "137",
                "taskId": "task3.json"
            }...,
        ],
        "task": "task3.json",
        "user": "quoter"
    },
]
```

## Разработанные для оценки качества инструменты

### Тул для генерации искаженных контуров
Тул выполняет распознавание фрагмента спутникового слоя и записывает распознанные полигоны в shape-файл.
```
Usage: recognition_samples_gen --bbox <value> --mode <value> --semseg_path <value> --edge_detect_path <value> --out_dir <value> --out_layer <value> <options...>

  --bbox <value>               region bbox in format lt_x,lt_y~rb_x,rb_y in geodetic coordinates
  --mode <value>               recognition algorithm, one of: edge, rectangle
  --semseg_path <value>        path to the gdef file for semantic segmentation net
  --edge_detect_path <value>   path to the gdef file for edge detector net
  --out_dir <value>            directory for output layer
  --out_layer <value>          output file name
  --start_id <n>               Initial id for output object
```

Исходники: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/autocart/qa/recognition_samples_gen

### Тул для вычисления значения метрики
Тул принимает на вход shape-файлы с эталонной разметкой, а также оцениваемые полигоны (в виде заданий стенда), находит для каждого оцениваемого полигона соответствующий полигон из эталонной разметки, с которым [мера Жаккара](https://ru.wikipedia.org/wiki/Коэффициент_Жаккара) наибольшая, затем вычисляет для этой пары параметры аффинного преобразования и значение метрики. Результаты выводятся в стандартный вывод, каждая строка содержит следующие значения:
* `task_id` -- идентификатор задачи станда разметки
* `object_id` -- идентификатор объекта
* `IoU` -- мера Жаккара
* `metric` -- значение метрики
* `residual` -- невязка между оцениваемым полигоном и эталонным, искаженным подобранным аффинным преобразованием
* `shift_x`
* `shift_y`
* `theta`
* `scale`

```
Usage: metric --model_path <value> <options...>

  --reference_polygons_dir <value>    path to shape file with reference polygons
  --markup_tasks_dir <value>          dir with markup tasks
  --region_boundary <value>           file with wkt boundary of region
  --model_path <value>                path to model file
```
Исходники: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/autocart/qa/metric/bin


### Библиотека для анализа результатов
Исходники: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/autocart/qa/metric/jupiter/utils

## Процедура приемки метрики
1. Сгенерировать набор искаженных контуров для нескольких целевых регионов в Турции (по 1К примеров на каждый <регион, алгоритм>)
2. Разметить качество распознавания на стенде силами картографов.
3. Получить с помощью тула метрику качества для искаженных контуров.
4. Проанализировать результаты.

Для приемки метрики использовались два алгоритма распознавания полигонов зданий по спутниковым снимкам, а также эталонные датасеты контуров зданий для 4-х типов застройки в Турции:
  1. [редкая аккуратная застройка](https://h.yandex-team.ru/?https%3A%2F%2Fmpro-and.maps.yandex.ru%2F%3Fll%3D29.787742%252C40.714095%26z%3D15%26l%3Dmp%2523sat%26branch%3D0%26activity%3Deditor%26id%3D4500810373)
  1. [нерегулярная частая полудеревенская застройка](https://h.yandex-team.ru/?https%3A%2F%2Fmpro-and.maps.yandex.ru%2F%3Fll%3D29.958511%252C40.776757%26z%3D16%26l%3Dmp%2523sat%26branch%3D0%26activity%3Deditor%26id%3D4500810933)
  1. [крупные здания средней степени сложности планировки](https://mpro-and.maps.yandex.ru/?ll=29.057394%2C40.189466&z=15&l=mp%23sat&branch=0&activity=editor&id=4500811203)
  1. [высотная застройка (в т.ч. с крышами не красного цвета)](https://mpro-and.maps.yandex.ru/?ll=30.683212%2C36.892245&z=15&l=mp%23sat&branch=0&activity=editor&id=4500811093)

Для каждого региона эталонного датасета каждым из алгоритмов распознавания был сгенерирован набор из 1000 контуров для оценки.
```
./recognition_samples_gen \
    --bbox  29.776712,40.711542~29.798603,40.727759 \
    --mode rectangle \
    --semseg_path ../../models/sem_segm.gdef \
    --edge_detect_path ../../models/edge_detection.gdef \
    --out_dir out \
    --out_layer bld_1_rectangle \
    --start_id 1


./recognition_samples_gen \
    --bbox  29.951769,40.772453~29.965440,40.781147 \
    --mode rectangle \
    --semseg_path ../../models/sem_segm.gdef \
    --edge_detect_path ../../models/edge_detection.gdef \
    --out_dir out \
    --out_layer bld_2_rectangle \
    --start_id 10000


./recognition_samples_gen \
    --bbox  29.051176,40.177976~29.072333,40.193196 \
    --mode rectangle \
    --semseg_path ../../models/sem_segm.gdef \
    --edge_detect_path ../../models/edge_detection.gdef \
    --out_dir out \
    --out_layer bld_3_rectangle \
    --start_id 20000


./recognition_samples_gen \
    --bbox  30.680496,36.886977~30.695263,36.898760 \
    --mode rectangle \
    --semseg_path ../../models/sem_segm.gdef \
    --edge_detect_path ../../models/edge_detection.gdef \
    --out_dir out \
    --out_layer bld_4_rectangle \
    --start_id 30000

./recognition_samples_gen \
    --bbox  29.776712,40.711542~29.798603,40.727759 \
    --mode edge \
    --semseg_path ../../models/sem_segm.gdef \
    --edge_detect_path ../../models/edge_detection.gdef \
    --out_dir out \
    --out_layer bld_1_edge \
    --start_id 40000


./recognition_samples_gen \
    --bbox  29.951769,40.772453~29.965440,40.781147 \
    --mode edge \
    --semseg_path ../../models/sem_segm.gdef \
    --edge_detect_path ../../models/edge_detection.gdef \
    --out_dir out \
    --out_layer bld_2_edge \
    --start_id 50000


./recognition_samples_gen \
    --bbox  29.051176,40.177976~29.072333,40.193196 \
    --mode edge \
    --semseg_path ../../models/sem_segm.gdef \
    --edge_detect_path ../../models/edge_detection.gdef \
    --out_dir out \
    --out_layer bld_3_edge \
    --start_id 60000


./recognition_samples_gen \
    --bbox  30.680496,36.886977~30.695263,36.898760 \
    --mode edge \
    --semseg_path ../../models/sem_segm.gdef \
    --edge_detect_path ../../models/edge_detection.gdef \
    --out_dir out \
    --out_layer bld_4_edge \
    --start_id 70000
```

Сгенерированные контуры были залиты на стенд для разметки их качества.
```
python3 generate_task.py --data /home/quoter/devel/arcadia/maps/wikimap/mapspro/services/autocart/qa/recognition_samples_gen/out/bld_1_rectangle.shp --out_dir data/markup_tasks/ --prefix bld_1_rectangle --task_size 20 -n 50

python3 generate_task.py --data /home/quoter/devel/arcadia/maps/wikimap/mapspro/services/autocart/qa/recognition_samples_gen/out/bld_2_rectangle.shp --out_dir data/markup_tasks/ --prefix bld_2_rectangle --task_size 20 -n 50

python3 generate_task.py --data /home/quoter/devel/arcadia/maps/wikimap/mapspro/services/autocart/qa/recognition_samples_gen/out/bld_3_rectangle.shp --out_dir data/markup_tasks/ --prefix bld_3_rectangle --task_size 20 -n 50

python3 generate_task.py --data /home/quoter/devel/arcadia/maps/wikimap/mapspro/services/autocart/qa/recognition_samples_gen/out/bld_4_rectangle.shp --out_dir data/markup_tasks/ --prefix bld_4_rectangle --task_size 20 -n 50

python3 generate_task.py --data /home/quoter/devel/arcadia/maps/wikimap/mapspro/services/autocart/qa/recognition_samples_gen/out/bld_1_edge.shp --out_dir data/markup_tasks/ --prefix bld_1_edge --task_size 20 -n 50

python3 generate_task.py --data /home/quoter/devel/arcadia/maps/wikimap/mapspro/services/autocart/qa/recognition_samples_gen/out/bld_2_edge.shp --out_dir data/markup_tasks/ --prefix bld_2_edge --task_size 20 -n 50

python3 generate_task.py --data /home/quoter/devel/arcadia/maps/wikimap/mapspro/services/autocart/qa/recognition_samples_gen/out/bld_3_edge.shp --out_dir data/markup_tasks/ --prefix bld_3_edge --task_size 20 -n 50

python3 generate_task.py --data /home/quoter/devel/arcadia/maps/wikimap/mapspro/services/autocart/qa/recognition_samples_gen/out/bld_4_edge.shp --out_dir data/markup_tasks/ --prefix bld_4_edge --task_size 20 -n 50
```

Для распознанных полигонов была вычислена метрика их качества:
```
./metric --reference_polygons_dir ../../reference_data/out --markup_tasks_dir /home/quoter/devel/ymap-auto-markup/labeler-app/data/markup_tasks/  --model ~/devel/ymap-auto-markup/labeler-app/data/linear.model > bld_metrics.txt
```

Затем 5 экспертов-картографов выполнили разметку качества полигонов.

### Результаты разметки результатов распознавания
Всего были собраны 33186 оценки для 7654 уникальных контуров.

Средняя точность эксперта по сравнению со мнением большинства составила 85%.

user |	good |	bad |	precision
---|---|---|---
miryash@yandex-team.ru |   	6230 |	920 |	86%
Muhamadiev |              	4568 |	2926 |	85%
esnikonova  |             	4906 |	2707 |	87%
isk92  |                	2872 |	618 |   91%
zabyg17  |                	4497 |	2942 |	82%

Средняя точность по всем контурам составила 69%.

region | method | good | bad | good ratio
---|---|---|---|---
all | | 5264 | 2390 | 69%
1 | rectangle | 814 | 186 | 81%
1 | edge | 811 | 189 | 81%
2 | rectangle | 629 | 261 | 71%
2 | edge | 763 | 237 | 76%
3 | rectangle | 589 | 227 | 28%
3 | edge | 524 | 424 | 45%
4 | rectangle | 791 | 209 | 79%
4 | edge | 805 | 195 | 81%


### Оценка качества метрики
Из всех 7654 распознанных контуров только для 6055 из них в эталонной разметке нашелся соответствующий контур с ненулевой площадью пересечения, из них 75% по мнению большинства были расценены хорошими.

Распределение значений метрики среди хороших и плохих контуров показано на графике.

![](https://jing.yandex-team.ru/files/quoter/good_bad_scores.png)

ROC-кривая для метрики выглядит следующим образом:

![](https://jing.yandex-team.ru/files/quoter/roc.png)

Если использовать пороговое значение `0.40`, как это рекомендовано с пояснительной записке к метрике, то точность (accuracy) составит `52%`.
Максимальная точность `75%` достигается, если использовать пороговое значение `0.0`.

Из этого можно сделать вывод, что обученная модель слабо отличает плохие контуры от хороших.

Вот несколько примеров false-negative ошибок метрики:
1. метрика считает плохими все контура, в которых произошло ухудшение контура

![](https://jing.yandex-team.ru/files/quoter/Karta_2018-03-27_14-37-21.png)

2. метрика считает плохими даже случаи, когда смещение границ здания составило 2.5 м

![](https://jing.yandex-team.ru/files/quoter/Karta_2018-03-27_14-40-05.png)

3. метрика считает плохими все случаи, где смежные здания были объединены в одно

![](https://jing.yandex-team.ru/files/quoter/Karta_2018-03-27_14-42-21.png)

## Исследование полезности факторов афинного преобразования

Цель: сравнить качество классификатора, построенного на факторах аффинного преобразования в сравнении с baseline-классификатором, построенным на IoU.

Разделим накопленный нами датасет полигонов на три части: обучающий (80%), валидационный (10%) и тестовый (10%).

Обучим классификатор catboost на подобранных факторах аффинного преобразования и проверим на тестовом датасете:

![](https://jing.yandex-team.ru/files/quoter/metric_analysis_2018-03-27_15-29-32.png)

Обучим классификатор catboost на факторе IoU и проверим на тестовом датасете:

![](https://jing.yandex-team.ru/files/quoter/metric_analysis_2018-03-27_15-33-27.png)

Совместим все эти факторы, обучим и протестируем классификатор:

![]()

Сводные данные в одной таблице

factors | roc_auc | accuracy | threshold
---|---|---|---
affine | 0.75 +/- 0.02 | 0.80 +/- 0.02| 0.05
IoU | 0.78 +/- 0.02| 0.78 +/- 0.02 | 0.45
affine + IoU | 0.82 +/- 0.02 | 0.81 +/- 0.02 | 0.25


Можно сделать вывод, что при данном методе обучения классификатора факторы аффинного преобразования работают с тем же качеством, что и baseline-фактор IoU.
Использование совокупности этих факторов немного улучшает классификатор.


## Возможные сценарии использования метрики
Автоматическая метрика оценки качества контуров может потребоваться в следующих сценариях:
1. отслеживать малые изменения качества определенного алгоритма распознавания
2. сравнивать качество распознавания принципиально нового алгоритма распознавания в сравнении с текущим baseline-алгоритмом.

### Отслеживание малых изменений качества определенного алгоритма распознавания
1. Выполнить распознавание области, для которой есть эталонная разметка, необходимо не менее 3К контуров.
2. Загрузить полученные контуры на стенд и разметить их с помощью экспертов.
3. Для каждого распознанного контура вычислить факторы IoU, параметров аффинного преобразования.
4. Обучить модель классификатора на данных разметки.
5. Затем на каждой итерации изменения алгоритма распознавания вычислять значение метрики для каждого распознанного контура. По изменению интегрального значения метрики можно делать вывод о улучшении или ухудшении алгоритма распознавания.

### Cравнение качества распознавания принципиально нового алгоритма распознавания в сравнении с текущим baseline-алгоритмом

Пусть у нас есть текущий baseline-алгоритм распознавания, а также обученная для него метрика.
Нам дается принципиально новый алгоритм распознавания, задача состоит в том, чтобы сравнить его качество с baseline-алгоритмом.

В этом случае можно использовать обученную метрику, однако, поскольку новый алгоритм может привнести принципиально новые типы "искажений", которые метрика ранее не видела,  результат нужно обязательно валидировать экспертами.

Для валидации достаточно сгенерировать 1К контуров и разметить их экспертами.

