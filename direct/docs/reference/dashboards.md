# Полезные дашборды, доски

Статус документа: в разработке. 

Присылайте полезные дашборды через [форму обратной связи](https://forms.yandex-team.ru/surveys/51191/)
или [сразу вносите](https://a.yandex-team.ru/arc/trunk/arcadia/direct/docs/reference/dashboards.md?edit=true) в документацию
([подробная инструкция](../guide/dev/how-to-write-documentation.md) о её редактировании).

## Общее

Cycle time (статистика по времени между разными статусами тикетов):  
<https://datalens.yandex-team.ru/k9cxivluw5xah-metrika-cikl-tayma-servisov-otdela-poiskovyh-interfeys?tab=XV&state=8b7fc9ac451>

## Разработка


## Релизы

Релизный дашборд: <https://st.yandex-team.ru/dashboard/1249>


## Эксплуатация 

Главный мониторинговый дашборд app-duty: <https://solomon.yandex-team.ru/?project=direct&dashboard=direct-group-sre-tv>

Главный дашборд про непродакшен: <https://solomon.yandex-team.ru/?project=direct&dashboard=direct-np-main>

App-duty тикеты: <https://st.yandex-team.ru/dashboard/24555>

Графики [JobsApp](https://grafana.yandex-team.ru/d/nEv3DIDWk/jobs) для всех окружений (переключаются ссылками в правом верхнем углу)

Графики [IntapiApp](https://grafana.yandex-team.ru/d/5jjuvkAWz/intapi) для всех окружений (нужно изменить _оба_ селектора в левом верхнем углу)

Графики про [перловый транспорт в модерацию](https://monitoring.yandex-team.ru/projects/direct/dashboards/mon83qbja48sb3qobmm4?range=6h&refresh=60)

Графики про [перловый экспорт в БК](https://solomon.yandex-team.ru/?project=direct&dashboard=bs-export-perl&b=6h)

Дашборд по вычислительным ресурсам YT в подпулах direct_all: <https://solomon.yandex-team.ru/?project=direct&dashboard=yt_resources_dashboard&l.yt_cluster=hahn>

## Поддержка

Статистика по ZBP: <https://datalens.yandex-team.ru/idsyijcas48yd-direct?tab=6P3>


## Аварии { #incidents }

Статистика по инцидентам: <https://datalens.yandex-team.ru/aq299sisay946-direkt-incidenty>
([тестинг дашборда](https://datalens.yandex-team.ru/8jwlu1mfvc3s2-direkt-incidenty-dev)).

Инциденты в Трекере: <https://st.yandex-team.ru/dashboard/1555>


## За пределами Директа

### SBYT баннерной крутилки
[Дашборд SBYT](https://grafana.yandex-team.ru/d/YHGqmZ5Zk/bsmon-stat-yt-sbyt?orgId=1&refresh=5m).  
По нему можно удобно определять время наших инцидентов, связанных с отставанием статистики или задержкой в обработке логов БК.
