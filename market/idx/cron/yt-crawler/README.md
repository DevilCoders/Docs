# Об инструменте
Программа листит все операции запущенные в указанном пуле под указанным аккаунтом и собирает статистику. Вы должны указать пул, аккаунт, временной промежуток через таймстемпы, названия и тип статистик (sum, avg, count, max, min), тип операций (map, merge, erase, sort, reduce, mapreduce, remotecopy, joinreduce, vanilla). Дополнительно, предоставляются комманды с помощью которых происходил запуск операций или бинаря.

Примечание: утилита имеет смысл только для системных статистик https://yt.yandex-team.ru/docs/problems/jobstatistics#sistemnye-statistiki

# Пример

```
./yt-crawler --yt-proxy arnold --yt-pool market-testing-indexer --user robot-mrkt-idx-tst --from-time 1631191200 --to-time 1631191216 --sum user_job/cpu/user --type map
Using settings:
====================
Yt {
  Proxy: "arnold"
  # ProxyRole: ""
  # TokenPath: ""
  Pool: "market-testing-indexer"
  # ClientLogPath: ""
}
User: "robot-mrkt-idx-tst"
FromTime: 1631191200
ToTime: 1631191216
Type: Map
Sum: "user_job/cpu/user"
# Avg: 
# Count: 
# Max: 
# Min: 
====================
INFO: 2021-09-13 17:51:02.535 +0300 main.cpp:270 Finished
cat operations.json 
[{"executable_path":"/usr/lib/yandex/promo_details_collector","id":"86ef70bf-5947ec92-41103e8-a028d2d7","summary":{"user_job/cpu/user/sum":404614},"title":"NMarket::NPromoDetailsCollector::TTemporaryPromoTableMapper"}]
```
