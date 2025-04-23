##Запустить локально на данный с yt
```
yt read 
    //home/logfeller/logs/mail-so-antifraud-log/stream/5min/2020-12-15T11:40:00
    --proxy hahn.yt.yandex.net
    --format json
| grep '"request":"score"'
| grep '"subchannel":"MY_CHAN"'
| head -n 10000 
| ./run.sh analyze binbase.txt std://in ./antifraud/channels.conf std://out
```
