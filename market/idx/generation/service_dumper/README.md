# service_dumper

Программа принимает на вход данные от service_reducer и дапит их на диск в fb64.

Пример запуска:
```shell
./service_dumper --debug \
--yt-proxy arnold \
--yt-token-path /home/iurik/.yt/testing \
--yt-proxy-role=market \
--input //tmp/iurik/multistock_reduce/0000 \
--output /home/iurik/tmp
```