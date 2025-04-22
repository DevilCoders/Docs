# Reset Source State
Инструмент для сброса состояния по читаемому источнику. В частности, для цезаря и баззарда скрипт 
очищает папку `consuming system`'ы на YT и очищает `sequence numbers` по соответствующим `source ids` в офсетах воркера.
Примеры использования:  
+ CaeSaR: 
`./reset_source_state -v --service caesar --caesar-key 11 --source-name shubert/offer_base`
+ Buzzard: `./reset_source_state -v --service buzzard --buzzard-stand prestable --source-name crypta/dmp-segments-log`

`./reset_source_state -h` для более подробного описания.
 

TODO:
1. ДОБАВИТЬ РЕТРАИ НА DROP SOURCE IDS
2. ДОБАВИТЬ ПРОВЕРКУ НА СУЩЕСТВОВОВАНИя В ОФСЕТАХ УДАЛЯЕМЫХ SOURCE IDS
