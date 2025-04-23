# База знаний по техническим вопросам
* [Как перевести свой Nile-скрипт на Nile over YQL?](nile-over-yql.md)
### Как запускать недельные и месячные расчеты
Некоторые расчеты мы хотим запускать, когда:
* закончился период (например, наступил последный день месяца) и 
* готовы дневные данные для этого дня

Для этого можно использовать артефакты, которые создаются в последний день месяца или в последний день недели (воскресенье). Артефакты хранятся в [`/maps/analytics/tools/calendar-helpers`](https://reactor.yandex-team.ru/browse/resolve?path=%2Fmaps%2Fanalytics%2Ftools%2Fcalendar-helpers)

* Пример [недельной реакции](https://a.yandex-team.ru/arc_vcs/maps/analytics/legacy/nile/statadhoc-10453-geosearch-type-source-geography-report/lama.yaml?rev=404b4750512bb03b1cbf807b86f10cbbd659093c#L49) и использования недельного артефакта
* Тикет разработки: [MAPSINFRA-3005](https://st.yandex-team.ru/MAPSINFRA-3005)
