Подготовка трейн-пула для обучения модели
---

Процесс подготовки трейн-пула для обучения модели предсказания eta.
Создает одну табличку на день. Для создания таблички за день D использует треки за день D

В процессе работы выполняет следующие действия:
- обрезка треков с начала и конца
- фильтрация и семплирование
- генерация фич для моделей

Параметры этих действий задаются через конфиг(см. директорию [`conf`](conf)).

### Результаты

[Тестинг future-model](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/whole_track_model/pools/future)
[Продакшн future-model](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/whole_track_model/pools/future)

[Тестинг statistical-data-model](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/whole_track_model/pools/on_travel_times)
[Продакшн statistical-data-model](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/whole_track_model/pools/on_travel_times)

[Тестинг user-traits-model](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/whole_track_model/pools/user_traits)
[Продакшн user-traits-model](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/whole_track_model/pools/user_traits)

[Тестинг taxi-model](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/whole_track_model/pools/taxi)
[Продакшн taxi-model](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/whole_track_model/pools/taxi)
