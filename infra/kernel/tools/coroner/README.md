# coroner 
kernel logs query client
- [WIKI] (https://wiki.yandex-team.ru/kernel/#coroner)


## Usage guide
List hosts in rtc.stage-prestable walle prestable group
```
coroner -w rtc.stage-prestable --list-hosts
```
Query kernel logs for given walle group
```
coroner -w rtc.stage-prestable -p
```

Querry local server's logs for a given host kernel1.search.yandex.net 
```
./coroner -H kernel1 -p -L
```
