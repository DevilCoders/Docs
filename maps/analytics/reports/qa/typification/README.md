# Отчет метрики типизации задач тестирования в картах

График отображает процент [типов задач](https://wiki.yandex-team.ru/maps/testing/tipizacija-zadach-bjak/#dljaocheredimapsui), отдаваемых в асессоров.
Графики представлены в:
| Сервис | Ссылки |
|:------------- |:-------------:|
| Реактор БЯК | https://reactor.yandex-team.ru/browse/resolve?path=/maps/analytics/reports/qa/typification/web-maps/monthly |
| Отчёт для БЯК | https://stat.yandex-team.ru/Maps/qa/typification/ |
| Отчёт для НЯК | https://stat.yandex-team.ru/Maps_Plus_Beta/QA/Confeta/typification |

## Основная информация
Отчет собирает данные из Стартрека, выгруженные в YT.

Тип задач определяется соответствующим [тегом](https://wiki.yandex-team.ru/maps/testing/tipizacija-zadach-bjak/#dljaocheredimapsui), который проставили тестировщики.
Вовлеченность асесессоров так же определяется тегами. Возможна частичная вовлеченность, полная или ее отсутствие.
Фильтрами собираем:
* задачи каждого типа
* с резолюцией fixed, зарезолвленные в прошедшем месяце
* каждый тип фильтруем по степени вовлеченности

## Делаем в рамках задачи
https://st.yandex-team.ru/MAPSINFRA-2301
https://st.yandex-team.ru/GEOMETRICS-146
