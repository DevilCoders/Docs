# yd
https://deploy.yandex-team.ru/stages/vh-static-indexer/config/du-zen-streams-generator

# monitorings
https://yasm.yandex-team.ru/panel/_J5WxdI/

# output tables
https://yt.yandex-team.ru/arnold/navigation?path=//home/video-hosting/zen-tables

# diff between v1 and v2
v1 writes output streams separated by commas in 1 string.
v2 writes ouput streams in json with format:
```
{
    "streams": []
}
```

# how to debug
change `resultTable` in config.json to your path (otherwise it overwrites production tables)
build
./zen-streams-generator client-mode ./config.json --schema ugc --connection-string 'connection-string to pg ugc' --unistat-port 8010
