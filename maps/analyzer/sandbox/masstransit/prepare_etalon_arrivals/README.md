Подготовка эталонных прибытий общественного транспорта на остановки
---

Процесс создает одну табличку на день, содержащую информацию о времени прибытия транспорта на остановки. Для расчета таблички используются треки (привязанные ОТ-сигналы) за тот же день. Алгоритм интерполирует время проезда между привязанными сигналами с учетом времени стояния на остановке и исходя из предположения о равной скорости движения на остальных сегментах.
Параметры задаются через конфиг (см. директорию [`conf`](conf)).

### Результаты

Testing: [//home/maps/jams/testing/masstransit/etalon/arrivals](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/masstransit/etalon/arrivals)<br>
Production: [//home/maps/jams/production/masstransit/etalon/arrivals](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/etalon/arrivals)
