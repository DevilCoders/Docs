##На этом сайте можно найти

   * [информацию о коллекциях MongoDB](./Mongo collections/Index/)
   * [документацию, относящуюся к репликации и загрузке данных Яндекс.Такси в YT.](./Yt tables/Index/)
   * [описание протокола](./cpp-services-description/) и [список сервисов](./Backend-cpp services/Index/) в backend-cpp
   * [список сервисов uservuices](./Uservices/Index/)
   * [список сервисов backend-py3](./Backend-py3/Index/)
   * [описание сервиса replication](./replication-docs/replication-service/)

Можно воспользоваться поиском по сайту (вверху слева).


##[Коллекции MongoDB](./Mongo collections/Index/)

Коллекции отсортированы по connection для более удобной навигации.


##[Репликация](./Yt tables/Index/)

За процесс репликации отвечает
[подгруппа разработки платформы управления данными](https://staff.yandex-team.ru/departments/yandex_distproducts_browserdev_mobile_taxi_9720_3279_dep42758/).
Если тебе не удалось найти ответ на интересующий тебя вопрос на этом сайте, то 
смело обращайся к любому члену нашей подгруппы.

Общее описание самого процесса репликации и инструкция по добавлению в него 
новых источников/полей на данный момент живет в документации: 
<https://pages.github.yandex-team.ru/taxi/schemas/Taxi_Documentation/replication-docs/replication-service/>

Описание процесса загрузки данных в YT (из кеша C++ сервисов):
<https://wiki.yandex-team.ru/taxi/backend/YtUploadCxx/>
 
Расположение описания таблицы соответствует ее пути в YT. При этом 
префикс **map_reduce** означает, что таблица реплицируется на **hahn** и 
**arnold**, а **runtime** — что на **seneca-man**, **seneca-sas** и 
**seneca-vla**.
