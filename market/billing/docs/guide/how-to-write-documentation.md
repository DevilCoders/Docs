# Написание, отладка и выкладка документации

**Разовая подготовка к работе:** см. ниже раздел [{#T}](#get-sources)

## Написать новые или поправить существующие страницы

Если добавляешь новую страницу, ее надо записать в файл `toc.yaml`, иначе она не попадет в выкладку.

Если сомневаешься, где в файлах и в оглавлении разместить новую страницу &mdash; спроси lena-san@ или hmepas@

Синтаксис разметки: <https://github.com/yandex-cloud/yfm-transform/blob/master/DOCS.ru.md>

## Собрать и посмотреть документацию локально

Все команды запускать из каталога `market/billing/docs`.

Собрать доку:
```
ya make
```
В результате образуется файл `docs.tar.gz`.

Распаковать собранное в каталог `result`:
```
rm -rfv result && mkdir -p result && tar -xvf docs.tar.gz -C result
```

Дальше можно:
- открыть файл `result/index.html` браузером
- запустить простой http-сервер и открыть доку через него

Вариант с http-сервером: `python -m SimpleHTTPServer 5000` (Python 2) или `python3 -m http.server 5000` (Python3) и браузером открыть <http://127.0.0.1:5000/result/> 

## Показать новонаписанную доку коллегам

Сделать pull-request в Аркадии.
Через пару минут в PR придет робот `robot-cozmo` и запостит комментарий со ссылкой на сборку из этого PR.

Комментарий выглядит так:
```
DOCS deployed: market-billing by Sandbox task NNNNN
```


## Задеплоить документацию

Закоммитить/замержить правки в транк. Через несколько минут правки автоматически выедут на <https://docs.yandex-team.ru/market-billing/>


## Особые случаи

### PlantUML диаграммы { #plantuml }

В целом они работают. Документация: <https://docs.yandex-team.ru/docstools/custom-plugins/plantuml>

Пример:

@startuml
Alice -> Bob: Authentication Request, аутентификационный запрос
Bob --> Alice: Authentication Response
Alice -> Bob: Another authentication Request
Alice <-- Bob: another authentication Response
Алиса -> Bob: и еще запрос
@enduml

Особенности:
* невозможно локально посмотреть получающийся svg; пока рекомендация -- делать PR и смотреть схемы там. Релевантный тикет <https://st.yandex-team.ru/DOCSTOOLS-1060>


## Разовая подготовка к работе: получить исходники { #get-sources }

Надо сделать один раз.

Варианты: использовать arc или svn. Рекомендуется пользоваться arc-ом.

### arc

Ничего особенного делать не надо, все уже есть в рабочей копии.

### svn

{% cut "Если почему-то понадобилось работать именно с svn" %}

Если еще нет аркадийной svn-рабочей копии &mdash; сделать ее:
```
svn cat svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/ya | python - clone
```
Образуется каталог `arcadia`. Если хочется каталог с другим именем:
```
svn cat svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/ya | python - clone my_arcadia
```

Из корня аркадийной рабочей копии (`arcadia` или `my_arcadia` из предыдущего пункта):
```
ya make -j0 --checkout tools/mkdocs_builder
ya make -j0 --checkout market/billing/docs
```

`market/billing/docs` -- собственно исходники документации  
`tools/mkdocs_builder` -- тулзы, чтобы работала локальная сборка

{% endcut %}


## Ссылки { #links }

* Синтаксис разметки: <https://github.com/yandex-cloud/yfm-transform/blob/master/DOCS.ru.md>
* Инструкция по заведению проекта в docs (для Маркет-Биллинга уже сделано): <https://docs.yandex-team.ru/docstools>
* PlantUML диаграммы
  * Документация: <https://docs.yandex-team.ru/docstools/custom-plugins/plantuml>
  * Тикет, в котором их делали: <https://st.yandex-team.ru/DOCSTOOLS-25>
  * Тикет про локальные svg <https://st.yandex-team.ru/DOCSTOOLS-1060>
