# Генерация набора данных для проверки (sanity check) модели

Утилита принимает на вход 2 параметра:
- `-d` - дата сигналов, из которых будет сгенерирован набор данных для проверки.
  Формат сигналов - `yyyy-mm-dd`.
- `-o` - директория на YT, в которую будут помещены все результаты работы утилиты.

[Граф работы утилиты](https://jing.yandex-team.ru/files/kuzns/Sanity_check.png)

В качестве входных данных используются:
- [road_graph_traits](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/road_graph_traits) (выбираются по дате из входного параметра)
- [realtime_jams](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/realtime_jams) (выбираются по дате из входного параметра)
- [Сигналы](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/yatransport-prod/production/signals) (выбираются по дате из входного параметра)
- [Прибытия](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/etalon/arrivals) (выбираются по дате из входного параметра)
- [data.mms](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/data) (выбирается из атрибутов прибытий)
- [statistical_data.fb](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/statistical_data) (выбираются с помощью [функции из toolkit](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/toolkit/lib/sources.py?rev=r9083332#L661))
- [События](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/quality/events/metrika) (выбираются по дате из входного параметра)

Утилита случайным образом выбирает маршруты, таким образом, чтобы количество сигналов в результате было примерно 5-6 млн.
По выбранным маршрутам создается набор id ниток, присутствующий в выходном наборе данных.
Этот набор ниток используется для фильтрации прибытий, road_graph_traits, realtime_jams.
