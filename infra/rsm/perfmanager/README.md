# Perf Manager

### GUI
[Top Kernel funcs](https://datalens.yandex-team.ru/xzjgwl5kp1e4q-dash-kern)
[Top User funcs]https://datalens.yandex-team.ru/dfzhp8sqjhhs6-dash-user)

### Storage
[Logbroker](https://logbroker.yandex-team.ru/logbroker/accounts/rtcsysdev/perfmanager?page=browser&type=directory)
[YT top log](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/rtc-perfmanager-top-log)
[YT stat log](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/rtc-perfmanager-stat-log)

## Monitoring
* [Hostman](http://hm-prestable.in.yandex.net/units/yandex-perf-manager)

## Testing
### Check changed schema
cd logfeller/bin/stdin_parser
ya make --checkout
echo '<json>' | ./logfeller-stdin-parser --parser rtc-perfmanager-stat-log --configs ../../configs/parsers

