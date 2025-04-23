# Статистика по релизам

## Cycle tyme (время между статусами) { #cycle-time }

Все ссылки на примере релизов perl-Директа.
Есть фильтры по другим большим приложениям: выпадушка `Фильтр`, фильтры называются `DIRECT: Releases <приложение>`.

Окно для скользящего среднего лучше выбирать 28 дней, процентили — 50-ю и 95-ю. 

От создания до закрытия: <https://datalens.yandex-team.ru/k9cxivluw5xah-metrika-cikl-tayma-servisov-otdela-poiskovyh-interfeys?tab=XV&state=d640f8ae424>

От начала до окончания тестирования: <https://datalens.yandex-team.ru/k9cxivluw5xah-metrika-cikl-tayma-servisov-otdela-poiskovyh-interfeys?tab=XV&state=3c6c9821520>


## Слагаемые времени тестирования релизов { #testing-time-factors }

<https://javadirect-dev.yandex-team.ru/statistics/releases_table?app=java-web&number=40>

Если Cycle time научатся отслеживать не только статусы, но и простановку тегов, то можно будет использовать их. 


## Гистограммы слагаемых времени тестирования { #testing-time-factors-dynamics }

<https://javadirect-dev.yandex-team.ru/statistics/releases_pie_chart?app=java-web&number=3&block_size=5>


## Длительность автосборок { #autoreleases-metrics }

<https://direct.yandex.ru/logviewer/short/3xFM3dxO3YLp8L> , дату менять на нужную.  
Кроме длительности записывается успех/неуспех сборки. 

