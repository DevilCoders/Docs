### Статистика по абсолютам

Тула берёт карточные данные и по ним считает статистику:
* абсолютное количество объектов в разбиении по разным категориям и регионам
* суммарную длину линейных объектов

Результаты записываются в отчёты в стате:
* [Количество объектов](https://stat.yandex-team.ru/Maps.Wiki/KPI/AbsoluteValues/ItemsCount)
* [Длина линейных объектов](https://stat.yandex-team.ru/Maps.Wiki/KPI/AbsoluteValues/ItemsLength)


В нирване ежедневно запускается из воркфлоу `absolute_values-stat` в проекте [robot-wikimap-а](https://nirvana.yandex-team.ru/browse?selected=9363437)
В случае падений в нирване уведомление приходит в чатик [maps-wiki-monitoring](https://t.me/joinchat/BK1c6xAwU90UQg-SuAxgqg)

Для [ежедневного запуска](https://reactor.yandex-team.ru/reaction?id=9728606) из нирваны используется текущая актуальная версия [ymapsdf](https://doc.yandex-team.ru/ymaps/ymapsdf/ymapsdf-ref/concepts/about.html), которая лежит в [//home/maps/core/garden/stable/ymapsdf/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stable/ymapsdf/latest&)

Для этой версии актуальной всегда считается дата "сегодня", поэтому тула требует, чтобы именно такая дата была передана на вход, если явно не задан путь к данным.
В первый день каждых недели, месяца, года тула запишет в отчёт данные не только со `scale=daily`, но и с соответствующим `scale`.

При необходимости можно пересчитывать статистику по старым данным. Например, когда захотелось добавить новую категорию объектов и ретроспективно увидеть график изменения количества объектов в ней. Для удобства запуска есть скрипт `bin/recalculate_stat.sh`. Он пробегается по всем наборам данных в [//home/maps/core/garden/stable/ymapsdf_archive](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stable/ymapsdf_archive/&) и записывает данные для них в `stat-beta` со `scale=monthly`. Для записи в продакшен-стат нужно добавить опцию `--publish-production` в строку запуска. Чтобы пересчитать данные по одной таблице вместо полного набора можно опцией указать название таблицы.


### Нюансы
* при определнии региона, к которому относится конкретный адрес, берётся геометрическая принадлежность, а не административная. [Тикет](https://st.yandex-team.ru/NMAPS-14511) с обсуждением следующих из этого проблем. Правильно брать административную принадлежность.
