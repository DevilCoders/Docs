**Структура сети**

![Структура сети Unet](https://jing.yandex-team.ru/files/dolotov-e/unet.png)

Для нахождения ребер и вершин домов используется сеть, описанная в статье U-Net: Convolutional Networks for Biomedical Image Segmentation (Unet, https://arxiv.org/pdf/1505.04597.pdf).

Сеть Unet состоит из 4 стадий со свертками, после которых следуют слои с max pooling. Это позволяет снизить размер изображения в 16 раз. За четвертой стадией следуют еще две свертки. После этих сверток изображение начинает увеличиваться при помощи deconvolutinal слоев в 2 раза. После каждого увеличения выполняются еще две свертки. Особенностью архитектуры Unet является то, что к результату каждого deconvolution слоя присоединяется результат одной из первых четырех стадий. В конце выполняется свертка с ядром 1x1 и количеством каналов k, где k - число различных классов объектов.

Общая ошибка сети - сумма ошибок на всех ветках. Ошибка на одной ветке считается следующим образом:

![Функция ошибки](https://jing.yandex-team.ru/files/dolotov-e/iou_1.png)

![Функция ошибки](https://jing.yandex-team.ru/files/dolotov-e/iou_2.png)

#### Подготовка данных
Для обучения сети необходимо иметь следующие данные:
* Спутниковые снимки
* Разметку с полигонами домов

##### Скачивание данных
Для получения этих данных можно возпользоваться инструментом autocart/tools/ymapsdf_semseg_dataset_generator
Пример использования:
> ./ymapsdf_semseg_dataset_generator \
> --tile-source 'http://core-sat-internal.maps.yandex.net/tiles'  \
> --bbox '28.77,40.98~28.95,41.10'  \
> --zoom 18  \
> --connstr "dbname=garden host=garden-pgm-rus01h.tst.maps.yandex.ru user=mapsgarden password=gardenTst port=5432 options=--search_path=public,ymapsdf_yandex_and_tr_20171029_008718_17_7456629a"

**tile-source** - источник спутниковых снимков
**bbox** - координаты области
**zoom** - масштаб
**connstr** - параметры доступа к базе с разметкой. Актуальную информация можно посмотреть [здесь](https://garden.tst.maps.yandex-team.ru/). Необходимо смотреть строки со статусом 'completed'. Регион России - 'Russia', регион Турции - 'And Tr'

Результатом выполнения программы будут являться два файла:
* output.jpg - спутниковый снимок
* output.txt - разметка домов, дорог и т.д.

##### Растеризация разметки
Полученную разметку необходимо растеризовать.
Для этого можно воспользоваться инструментов autocart/tools/cnn_semseg_dataset_rasterizer

#### Запуск обучения

##### Локальный запуск
Для локального запуска обучения сети необходимо следующее:

* Создать папку **data** с обучающими данными.
* Прописать имена файлов с изображениями и разметкой в переменные окружения YTF_DATASET_IMAGE_FILENAME, YTF_DATASET_SEGM_FILENAME в файле run_local_train.sh
* Указать другие параметры обучения в run_local_train.sh
* Запустить run_local_train.sh

##### Запуск на нирване
Для запуска обучения на нирване необходимо выполнить следующие действия:

* Загрузить в нирвану архив с изображениями, указав при этом тип данных **Image**.
* Загрузить в нирвану архив с разметкой, указав при этом тип данных **Text**.
* Подать на вход [операции](https://nirvana.yandex-team.ru/operation/60e0dc6d-3cef-47fc-b836-b5e10c264f78/overview) два этих архива, указать в опциях операции необходимые параметры обучения, запустить выполнение графа.

Для просмотра логов в tensorboard необходимо выполнить следующий запрос:
https://tensorboard.nirvana.yandex-team.ru/api/board/createFromNirvana?instanceId=**instanceId**&blockCode=**blockCode**&endpointName=logs

**instanceId** можно узнать во вкладке **Details** в поле Workflow Instance (пример 9233a2e6-93cd-4c7b-9c89-48d98919bdcb)

**blockCode** код блока можно узнать во вкладке **Details** в поле Local ID (пример operation-1523961991714-11)

