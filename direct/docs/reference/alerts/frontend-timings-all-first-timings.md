# *First

Проверки на время рендеринга отдельных страниц, без учета запросов к бекенду.

Хост `direct.solomon-alert.direct-frontend-timings-all-first-timings`.

- [groupsFirst](https://juggler.yandex-team.ru/check_details/?host=direct.solomon-alert.direct-frontend-timings-all-first-timings&service=groupsFirst)
- [bannersFirst](https://juggler.yandex-team.ru/check_details/?host=direct.solomon-alert.direct-frontend-timings-all-first-timings&service=bannersFirst)
- [campaignsFirst](https://juggler.yandex-team.ru/check_details/?host=direct.solomon-alert.direct-frontend-timings-all-first-timings&service=campaignsFirst)
- [bannersEditFirst](https://juggler.yandex-team.ru/check_details/?host=direct.solomon-alert.direct-frontend-timings-all-first-timings&service=bannersEditFirst)
- [bannersEditCpcFirst](https://juggler.yandex-team.ru/check_details/?host=direct.solomon-alert.direct-frontend-timings-all-first-timings&service=bannersEditCpcFirst)
- [groupsEditCpcFirst](https://juggler.yandex-team.ru/check_details/?host=direct.solomon-alert.direct-frontend-timings-all-first-timings&service=groupsEditCpcFirst)
- [groupsEditFirst](https://juggler.yandex-team.ru/check_details/?host=direct.solomon-alert.direct-frontend-timings-all-first-timings&service=groupsEditFirst)
- [bannersEditCpmFirst](https://juggler.yandex-team.ru/check_details/?host=direct.solomon-alert.direct-frontend-timings-all-first-timings&service=bannersEditCpmFirst)
- [groupsEditCpmFirst](https://juggler.yandex-team.ru/check_details/?host=direct.solomon-alert.direct-frontend-timings-all-first-timings&service=groupsEditCpmFirst)
- [feedFiltersFirst](https://juggler.yandex-team.ru/check_details/?host=direct.solomon-alert.direct-frontend-timings-all-first-timings&service=feedFiltersFirst)
- [phrasesFirst](https://juggler.yandex-team.ru/check_details/?host=direct.solomon-alert.direct-frontend-timings-all-first-timings&service=phrasesFirst)
- [targetingsFirst](https://juggler.yandex-team.ru/check_details/?host=direct.solomon-alert.direct-frontend-timings-all-first-timings&service=targetingsFirst)
- [usersProfileFirst](https://juggler.yandex-team.ru/check_details/?host=direct.solomon-alert.direct-frontend-timings-all-first-timings&service=usersProfileFirst)

## Описание { #description }
Проверки не скорость рендеринга отдельных страниц.
Строится по графикам скорости в solomon (см. ссылки). 
Данные о времени рендеринга страниц фронт присылает в ручку `web-api/log/frontendTimings`.

## Решение { #solution }
Разбирательствами с причинами загорания этой проверки занимается дежурный фронта.

## Ссылки { #links }
- [Графики скорости](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-web&service=java-monitoring&l.host=CLUSTER&l.sensor=frontend_timing&l.func=*First&l.env=production&l.bin=*&graph=auto)
- [Алерт в соломоне](https://solomon.yandex-team.ru/admin/projects/direct/alerts/direct-frontend-timings-all-first-timings)
- [Агрегаты в juggler](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Ddirect.solomon-alert.direct-frontend-timings-all-first-timings)
