Построение и загрузка календаря в ecstatic и YT
---

Скачивает `xml` файлы для каждого `country_id`, делая запросы в [calendar.yandex-team.ru](https://calendar.yandex-team.ru), билдит fb-файлы календарей, затем загружает их на ecstatic в датасет `yandex-maps-calendar` и на YT в [`//home/maps/jams/production/data/calendar`](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/data)

Включаемый диапазон дат регулируется с помощью конфига и параметров запуска. По-умолчанию, полный календарь содержит период с 1970-01-01 по текущую дату + 1 год вперед, а light-версия – от текущей даты - 2 года назад до текущей даты + 1 год вперед.
