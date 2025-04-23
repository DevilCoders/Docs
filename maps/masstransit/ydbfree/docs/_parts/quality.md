# Метрика качества

_На текущий момент реализована только метрика качества прогноза прибытий на остановки. Над метрикой качества меток мы работаем в тикете https://st.yandex-team.ru/MAPSJAMS-3737_

__=> ПАНЕЛЬ С МЕТРИКАМИ ОТ: https://datalens.yandex-team.ru/mxcyjknqnfrqf-obshestvennyy-transport-ot <=__

## Общее описание
Метрика в конечном счете должна показывать удовлетворенность пользователя качеством сервиса, т.о. стоит использовать время, показываемое пользователю.
Для этого можно использовать события открытия пользователем карточки остановки.
Затем, для каждого маршрута, проходящего через эту остановку и имевшего актуальный прогноз, можно посчитать ошибку, исходя из показанного времени прибытия и реального.
Такую метрику можно посчитать как по онлайн-предсказаниям, полученным из логов сервиса, так и по оффлайн-предсказаниям, рассчитанных с помощью MapReduce.

Код процесса: [maps/analyzer/sandbox/masstransit/quality](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/sandbox/masstransit/quality)

## Источники данных
### Прогнозы:
* онлайн: [//home/maps/jams/production/masstransit/forecasts/arrivals](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/forecasts/arrivals)
* оффлайн: [//home/maps/jams/production/masstransit/quality/offline/forecasts](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/quality/offline/forecasts)

### Прибытия:
[//home/maps/jams/production/masstransit/etalon/arrivals](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/etalon/arrivals)

## События:
### AppMetrika
* сырые данные: [//home/logfeller/logs/metrika-mobile-log](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/metrika-mobile-log)
* обработанные данные: [//home/maps/jams/production/masstransit/quality/events/metrika](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/quality/events/metrika)

### Логи сервиса
* сырые данные: [//home/logfeller/logs/maps-log/1d](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/maps-log/1d)
* обработанные данные: [//home/maps/jams/production/masstransit/quality/events/service_log](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/quality/events/service_log)

### Сгенерированные
Генерируем события открытия карточки раз в минуту по всем остановкам; покрывают в т.ч. остановки, по которым нет событий от пользователей. Данные: [//home/maps/jams/production/masstransit/quality/events/generated](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/quality/events/generated)

Из событий AppMetrka нас в первую очередь интересует `map.select-transport-stop-placemark` (пользователь выбрал пин остановки), а точнее его момент времени и id остановки.
Из логов сервиса берем запросы к ручке `/v2/stop`.

## Алгоритм расчета
Обрабатываем записи из всех трех таблиц в порядке хода времени. По предсказаниям поддерживаем состояние виртуального "табло с прогнозами". Каждое событие ставим в очередь ожидания прибытия. Прибытиями "закрываем" ожидающие события.

В конечном итоге для каждого запроса у нас есть вектор прогнозов (пользователю в приложении доступны несколько прогнозов для одного маршрута) и вектор прибытий.
По этим данным можно посчитать множество метрик. В нашем случае считаем 2 вида ошибок:
- для пары первый прогноз + первое прибытие
- для каждого прогноза первое прибытие, время которого больше либо равно времени прогноза

Первый тип ошибок покрывает кейс, когда пользователь стоит на остановке и ждет автобус, ему ок, если автобус приедет раньше.
Второй тип ошибок покрывает случай, когда пользователь смотрит прогноз прибытия заранее, например из дома, и ему важно не опоздать, при этом можно прийти заранее.

Имеем потенциально 2 исключительных состояния:
1. Нет прогноза. В первом приближении просто считаем количество таких случаев. Можно использовать статическое расписание.
2. Нет прибытия. Такая ситуация может возникнуть и по разным причинам (ТС "пропало", неправильно определили нитку и пр.). Таких случаев должно быть достаточно мало, но их количество надо считать.

## Формат результата
Большие ошибки могут возникать в случаях, когда предсказанное ТС и приехавшее отличаются (по `vehicle id`), но для пользователя это не имеет большого значения, однако нам эту информацию следует сохранить, чтобы понимать природу ошибки.
Также сохраняем время расчета прогноза (или сигнала), чтобы понять как величина ошибки меняется с устареванием прогноза.
Промежуточно сохраняем все записи в `stats` перед агрегацией.

В итоговые метрики группируем ошибки по следующим параметрам:
* `predicted_clid` – предсказанный `clid` (только при наличии группировки по `clid`)
* `event_source` – тип событий (`metrika`, `service_log`, `generated`)
* `vehicle_predicted` – совпадает ли ТС с предсказанным (`exact` - совпадает, `any` - любое)
* `request_type` – тип ошибки (`next` – первый прогноз + первое прибытие, `promised` – прогноз + прибытие после)
* `horizon` – горизонт (разность между временем реального прибытия и текущим), в минутах

## Результаты
* [Тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/masstransit/quality)
* [Продакшн](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/quality)

## Старое описание
* [wiki-страничка](https://wiki.yandex-team.ru/users/ovchinkin/masstransit/quality-metrics/)
* [тикет на создание](https://st.yandex-team.ru/MAPSJAMS-3255)
