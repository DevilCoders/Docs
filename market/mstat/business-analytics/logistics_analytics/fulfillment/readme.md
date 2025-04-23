Директория группы **Аналитики складов и СЦ**
____

 Структура директории:
 1) [production](https://a.yandex-team.ru/arc/trunk/arcadia/market/mstat/business-analytics/logistics_analytics/fulfillment/production) - продовая папка
 2) [analytical](https://a.yandex-team.ru/arc/trunk/arcadia/market/mstat/business-analytics/logistics_analytics/fulfillment/analytical) - ad-hoc's и околопродовые скрипты
 3) [Тестовая папка](https://a.yandex-team.ru/arc/trunk/arcadia/market/mstat/business-analytics/logistics_analytics/fulfillment/testing) - тестовые скрипты, файлы итд

____

Как добавить YQL-скрипт:
1) Зайти в нужную папку
2) Нажать Create file, задать имя + расширение *.yql
3) Вставить текст YQL-скрипта
4) **Как создать папку**: На данном этапе можно отредактировать название файла и путь к нему: если в пути добавить папку, которой еще нет, то в пул-реквест она добавится автоматически.<br>
Например: <br>
`trunk/arcadia/market/mstat/business-analytics/logistics_analytics/fulfillment/readme.md`<br>
отредактировать на:<br>
`trunk/arcadia/market/mstat/business-analytics/logistics_analytics/fulfillment/**SUBCAT**/readme.md`<br>
То файл readme.md создастся в новой директории **SUBCAT**.<br>

5) В нирване скопировать [Workflow](https://nirvana.yandex-team.ru/flow/e1894359-2ed6-4984-a937-e56765d24d04/68729976-0258-456c-bcd4-2e7bda5de453/graph) в котором заменить путь к файлу скрипта и токены.
6) "Commit" -> "Send to review" -> "Ship" -> "Auto merge"
7) Ждем окончание пулл-реквеста
____

Для всего остального (удаление файлов, папок, копии, перемещение и т.д.) нужно поставить [Arc](https://docs.yandex-team.ru/devtools/intro/quick-start-guide).<br>
После установки Arc'a репозиторий будет доступен на декстопе, включая все действия с файлами/папками.<br>
Для этого в терминале вводим команды:<br>
```
arc mount ~/arcadia
cd ./arcadia/market/mstat/business-analytics/logistics_analytics/
arc checkout -b ‘name_branch'
<<внести нужные изменения>>
arc diff
arc add -A
arc status
arc commit -m "what are you doing»
arc pr create --push -m «what_are_you_doing_pr»
```
получаем ссылку - переходим - публикуем - ждем - одобряем - вы великлопены<br>
Более подробная информация на страничке [Arc](https://docs.yandex-team.ru/devtools/src/arc/workflow)'a.
