#### Инструмент для оценки качества семантической сегментации

Производит оценку качества классификации по нескольким критериям:

* **total_px_acc**      - общее попиксельное качество классификации
* **label_px_acc**      - попиксельное качество классификации для каждого класса из classes
* **mean_px_acc**       - усредненное по всем классам попиксельное качество классификации
* **mean_iou**          - усредненная по всем классам метрика intersection over union (IoU, https://en.wikipedia.org/wiki/Jaccard_index)
* **freq_weighted_iou** - взвешенная по классам метрика intersection over union

![Формулы метрик](https://jing.yandex-team.ru/files/dolotov-e/metrics.png)

Пример использования:
> python semseg_compare.py --label_map <map> --gt <path/to/gt/folder> --test <path/to/test/folder>

* label_map - текстовый файл, задающий соответствие между именем класса и его меткой. Файл состоит из строк формата: <class_name> <class_label>
* gt        - путь до папки с эталонной разметкой
* test      - путь до папки с файлами, для которых производится сравнение
