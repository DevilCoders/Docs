
Тулза для отправки урлов для принудительного переобхода в самоваре, в результате урл парсится в RTHUB и в DC отправляется свежий дикий оффер.
Прокачка происходит с продовым контекстом хоста из заданий на обход дикого веба.

Тулза позволяет перепрокачать урлы, на которых были проблемы, чтобы проверить, что проблема решена/актуальна.

Для запуска нужно заполнить переменную окружения TVM_TOKEN из вот этого секрета: https://yav.yandex-team.ru/secret/sec-01fnxn34q7mys2g7azf910cr75

Посмотреть на контекст, без отправки:
```
./wild_web_recrawl_sender --url <url> 
```

Отправить:
```
./wild_web_recrawl_sender --url <url1> --url <url2> --send
```
