# indoor metrics tool

Утилита предназначена для анализа качества покрытия маяками того или иного помещения

## Принцип работы:

* По заданному `indoor_plan_id` достается самый свежий `indoor-mrc` трек, который
был помечен как _тестовый_ и не учавствовал в восстановлении маяков для данного
`indoor_plan_id`.

* Используя знание о геометрии этажа и позиций маяков из .mms файла + информацию
о `ground_truth` траектории, нарисованной в nmaps производится рассчет насколько
хорошо геометрия покрыта маршрутами

* Используя знание об отмеченных пользователем барьерах собранные треки
разбиваются на сессии, в рамках которых позиционирование было непрерывно.
Отсекаются слишком короткие сессии (короче 30 секунд)

* Используя данные о собранных сигналах и сенсорах из `indoor-mrc` трека
производится рассчет `indoor` позиции и ее сравнение с `ground_truth`. Возможны 3
варианта: решение не посчитано, решение посчитано, но ошиблись этажом, решение
посчитано + этаж совпал + ошибка с реальной позицией окалась n-метров

* Используя знание об ошибках со всех траекторий производится предположение об
ошибках каждой точке геометрии. Возможны следующие варианты: предположение об
ошибках не может быть сделано из-за того, что недостаточно покрытие
`ground_truth` треками, решение не посчитано, решение посчитано, но ошиблись
этажом, решение посчитано + этаж совпал. Тут же производится подсчет количесва
переключений с этажа на этаж и время *холодного старта*

## Пареметры запуска:
   1. `--config` - Путь до
   [конфига](https://arcanum.yandex-team.ru/arc_vcs/maps/indoor/libs/config/cfg/i-config.development.xml?rev=r8178838
   "Пример конфига"). Конфиг нужен для подключения к БД и S3, чтобы утилита могла
   достать необходимую информацию

   2. `--radiomap` - indoor_radiomap_tiles_`version`.mms - файл с тайлами
   радиокарты. (Этот файл является частью `yandex-maps-indoor-radiomap` датасета
   в ecstatic). Так же его можно скачать из s3 (пример ссылки:
   http://s3.mds.yandex.net/maps-garden-files-stable/stable/indoor_radiomap/indoor_radiomap_tiles_21.05.24-0.mms.63ceb7a9-bc2a-11eb-a667-da6596ab8698))

   3. `--indoor_plan_id` - идентификатор схемы помещений в nmaps, для которого
   производится анализ

   4. `--percentile` - процентиль для рассчета средней ошибки

   5. `--print-debug` - опциональный параметр, позволяет распечатать в файлы
   различную информацию полезую для визуализации easyview и дополниетельного
   анализа

   6. `--device-type` - опциональный параметр, позволяет указать работу какого
   устройства мы пытаемся эмулировать? `(ios|android|android-old)`.
   (`android-old` - для версий android <= 8) По умолчанию будет выбран `android`

   7. `--provider` - опциональный параметр, позволяет выбрать провайдера
   геолокации из доступных вариантов: indoor|lbs (indoor - означает алгоритмы
   indoor-позиционирования, lbs - Google Location Services)

   8. `--iterations` - опциональный параметр, позволяет определить количество итераций
   для прогона алгоритма позиционирования (может понадобиться для получения более
   точных метрик)

   9. `--assignment-id` - опциональный параметр, позволяет указать id assignment'а,
   если необходимо прогнать алгоритм по старым данным или по какому-то специальному
   заданию (assignment id можно посмотреть в приложении mrc).

##  Пример запуска:
```
./radiomap-metrics-tool --config ../../libs/config/cfg/i-config.production.xml --radiomap ~/yandex-maps-indoor-radiomap/indoor_radiomap_tiles_21.05.05-0.mms --indoor-plan-id 3581350858 --print-debug true --device-type android
```

##  Пример вывода результатов:

```
./radiomap-metrics-tool --config ../../libs/config/cfg/i-config.production.xml --radiomap ~/tmp/prod-tiles.mms --print-debug false --device-type android --assignment-id 1844
 --indoor-plan-id 3439872869
 ```

| Level | 0-9m (%) | 10-19m (%) | 20-49m (%) | 50-99m (%) | 100+m (%) | No sol (%) | No sol (s) | Uncov GT (%) | Median (m) | Duration (s) | TFF (s) | Lvl hit | Lvl miss | Lvl switch |
| ---: | ----: | ---: | ---: | ---: | ---: | ----: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
|         -1 |      34.54 |      42.11 |       6.12 |       0.00 |       0.00 |       0.00 |          9 |        17.22 |               11.00 |          381 |   31.50 |         372 |            0 |          0 |
|          1 |      23.40 |      44.06 |      14.09 |       0.00 |       0.00 |       0.02 |         10 |        18.42 |               12.00 |          635 |   31.00 |         415 |          210 |          2 |
|  1_OUTDOOR |       0.63 |       0.26 |       0.13 |       0.02 |       0.00 |       1.92 |        452 |        97.03 |                0.00 |          482 |   92.00 |           0 |           30 |          0 |
|          2 |      18.57 |      37.80 |      29.26 |       0.00 |       0.00 |       0.00 |          9 |        14.37 |               17.00 |          680 |   31.00 |         647 |           24 |          2 |

Обозначения столбцов:
 * `Level` - универсальный идентификатор этажа;
 * `0-9m` - процент площади этажа, на котором ошибка лежит в интервале 0-9 метров;
 * `10-19m` - процент площади этажа, на котором ошибка лежит в интервале 10-19 метров;
 * `20-49m` - процент площади этажа, на котором ошибка лежит в интервале 20-49 метров;
 * `50-99m` - процент площади этажа, на котором ошибка лежит в интервале 50-99 метров;
 * `100+m` - процент площади этажа, на котором ошибка превышает 100 метров;
 * `No sol` - процент площади этажа, на котором алгоритм не смог определить местоположение устройства;
 * `Uncov GT` - процент площади этажа, на котором отсутствует ground truth;
 * `Median` - значение ошибки позиционирования, соответствующей указанной процентили (по умолчанию - медианная ошибка);
 * `Duration` - суммарная продолжительность обходов на данном этаже (в секундах);
 * `TFF` - среднее время до получения первоначального решения (от Time to First Fix);
 * `Lvl hit` - время в секундах, в течении которого был правильно определен этаж;
 * `Lvl miss` - время в секундах, в течении которого был **не**правильно определен этаж;
 * `Lvl switch` - количество переключений между этажами.

## Дополнительный вывод, полезный для анализа (ключ `print-debug`)

* `cat 3581350858/level_1/ground_truth_heatmap.yson | easyview` - отобразить
тепловую карту ошибок позиционирования (в проекции на `ground_truth`)

* `cat 3581350858/level_1/heatmap.yson | easyview` - отобразить тепловую карту
ошибок позиционирования (предсказанную на всю геометрию)

* `cat 3581350858/level_1/%task_id%.yson | easyview` - отобразить процесс
позиционирования отдельного `indoor-mrc` трека. (зеленым цветом отображается
`ground_truth`, синим - посчитанное положение)
