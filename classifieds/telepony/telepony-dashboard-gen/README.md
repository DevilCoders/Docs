Telepony Dashboard Generator
================
## Описание проекта

Модуль ответственный за генерацию дашбордов и графиков в Grafana.
Данный модуль не предназначен для развёртывания в промышленной среде.
"Сценарии" генерации запускаются локально с указанием адреса Grafana,
а так же указанием `token`'а доступа для Grafana, его можно найти в секретнице.      
`url` и `token` указываются в `dashboard.gen.config` файле

# Важно!!!
> Используемый `token` нельзя оставлять в конфиге при коммите в репозиторий. 
> 
> Перед коммитом проверь, что он удалён из конфига.
> [секрет](https://yav.yandex-team.ru/secret/sec-01epea0webryjhd46gnqy6nm2j/explore/version/ver-01epea0wek48yp13djygxzk89y)


## Сценарии генерации

В каждом сценарии участвуют:
* **GrafanaClient** - клиент направляющий запрос в grafana на создание дашборда с графиками 
* **Dashboard** - сущность дашборда с описанием создаваемых графиков (пример `GenerationExample`)
* **Panel** - панелька с графиками нужных метрик, алертами и пр.
* **Target** - описание построения графика (пример `CmeAutoDealersGrafanaPanelFactoryExample`)

# Важно!!!
> При указании правила Alert'а необходимо убедиться, что в grafana существует `handler` алерта,
> на которое ссылается код. Иначе алерт не будет создан
>
> Описание Alert задаётся в **Panel**

Пример создания дашборда так же есть
[здесь](https://github.com/mcsim4s/scalograf/blob/main/tools/src/main/scala/Demo.scala)
