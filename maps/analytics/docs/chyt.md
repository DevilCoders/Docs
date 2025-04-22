## ClickHouse over YT

| | |
|---|---|
| Документация | https://yt.yandex-team.ru/docs/description/chyt/about_chyt.html |
| Дашборд нагрузки | [Соломон](https://solomon.yandex-team.ru/?project=yt&cluster=hahn&service=yt_clickhouse&l.cookie=Aggr&l.operation_alias=maps_datalens_chyt&dashboard=chyt_v2) |
| Чат поддержки | https://t.me/joinchat/DPeS0xFdpaSZoCWTYnhnnw |

### CHYT подключения в DataLens
Создано два chyt-подключения
- [maps-analytics-chyt](https://datalens.yandex-team.ru/connections/ide2yl3tmhnsg-maps-analytics-chyt) - основное поделючение для продакшен датасетов
- [maps-analytics-chyt-no-cache](https://datalens.yandex-team.ru/connections/ym4xf2m7ma4yr-maps-analytics-chyt-no-cache) - подключение без кеширования графиков. Используется для разработки дашбордов или для графиков, где данные обновляются чаще чем раз в 1 час.

Загрузку подключений можно смотреть на [дашборде](https://datalens.yandex-team.ru/j567qewsio40c-oko-dashbordov-analitik-kart?tab=mx).
