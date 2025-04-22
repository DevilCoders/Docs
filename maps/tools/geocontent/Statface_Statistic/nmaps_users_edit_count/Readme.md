Тул производит расчет статистики по правкам пользователя NMAP

Для расчета берутся таблицы:
* [Количество правок у пользователя на текущую дату](https://yt.yandex-team.ru/hahn/navigation?path=//home/geo-analytics/afanasieva/nmaps-beginners-dump-log/)
* [Лог пользователей NMAP](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/nmaps-users-dump-log/1d/)
* [Лог пользовательских правок](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/nmaps-edits-log/1d/2020-07-13)

Вывод отчета в стат:
* [Пользователи и правки](https://stat.yandex-team.ru/Maps.Wiki/Others/NmapsAnalytics/NmapUserCommit?scale=d&geo_path=_in_table_&status_path=%09_total_%09&action_path=%09_total_%09&object_path=%09_total_%09&max_distance=1&_incl_fields=count_uniq_puid&_incl_fields=count_uniq_commit_id&_incl_fields=count_uniq_object_id&_period_distance=1)

Скрипт запускается сам раз в день и делает расчет за вчерашнюю дату, либо запускается вручную за определенную дату.
