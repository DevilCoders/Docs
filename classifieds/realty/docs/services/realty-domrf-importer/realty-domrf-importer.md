### Назначение

Периодически забирает данные о ЖК из сервиса наш.дом.рф
Унифицирует полученные данные(обогащение siteId, houseId, загрузка картинок)
Формирует ресурс для обогащения ЖК

### Схема работы

Регулярная таска раз в сутки прокачивает все ЖК из наш дом рф через унификатор.
В унификаторе ЖК обогащается site и houseId на основании гео координат, загружает новые картинки(смотрим на то, что прокачали в прошлой версии ресурса)
Получившиеся данные записываем в ресурсе в ResourceService. Для аналитиков из этого ресурса формируется выгрузка в yt(https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/realty/testing/export/resources/domrf_complex)
