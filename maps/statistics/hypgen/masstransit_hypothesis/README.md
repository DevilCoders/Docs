masstransit_hypothesis
======================

Процесс, генерирующий гипотезы об изменении ниток ОТ на основании 
результатов привязки к существующей статике живых сигналов.

Сделано в рамках задачи 
https://st.yandex-team.ru/GEODA-23

Подробное описание:
https://wiki.yandex-team.ru/viktormatjuxin/202112-mthypothesis/

Запуск:
1) Create folder `bin/data`
2) Create `bin/hypothesis`
3) Copy `telegram_config.json` to `bin`
telegram_config.json contains information about bot_token and telegram chat_id
example of telegram.config:
```
{
"bot_token": "12345:AA",
"chat_id": "12345",
}
```
instead telegram.config you can use -t and -c keys when run script

4) 
```
ya make --checkout /home/vam1543/arcadia/maps/analyzer/data/coverage/
ya make --checkout /home/vam1543/arcadia/maps/analyzer/data/geobase/
```
5) 
```
make_and_send_hypothesis -w -u
```
