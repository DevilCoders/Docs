## Какие здесь тесты?

Прямо сейчас есть юнит-тесты на класс TRequestProcessor.
В них проверяется, что на заданный запрос был правильно сформирован объект TSportWizardRequestParams (т.е. выбран нужный матч, нужный турнир и т.п.) 
Каждому такому тесту на вход подается контекст запроса из apphost.

## Как запустить?
```
ya make -t
# локально может долго работать, тогда так:
ya make -t --test-disable-timeout
```

## Как написать юнит-тест?

#### 1. Сформировать контекст apphost-запроса

Тут можно пробовать несколько вариантов:
1. Задать в поиск запрос с параметрами `&json_dump_requests=BIATHLON`, в дампе найти элемент с типом `biathlon_setup`, и у этого элемента взять поле `global_ctx`.
Прямо сейчас это можно сделать примерно таким однострочником:
```
curl 'https://yandex.ru/search/?lr=213&text=лига%20чемпионов&json_dump_requests=BIATHLON' | ya tool jq '.WEB_SEARCH.WEB1.BIATHLON.requests[] | select(.type == "biathlon_setup") | .binary.global_ctx' | less
```
2. Можно раздампить контекст на локальной бете, т.е. то, что приходит в источник сюда:
https://a.yandex-team.ru/arc/trunk/arcadia/extsearch/wizards/sport_proxy/worker.cpp?rev=5076484#L56

#### 2. Залить контекст запроса в sandbox

Нужно сохранить контекст в json-файл с осмысленным именем (например, `request_champions_league.json`).
Затем залить командой вида:
```
ya upload --ttl=inf request_champions_league.json
```

Команда выдаст id полученного ресурса. Затем нужно добавить этот ресурс в ya.make
```
   sbr://<resource_id> # request_champions_league.json
```

#### 3. Написать проверки в классе юнит-теста

В юнит-тесте залитый контекст будет доступен под тем именем, которым он был назван в п. 2 (например, `request_champions_league.json`).
Пишем код по подобию с существующими проверками.
