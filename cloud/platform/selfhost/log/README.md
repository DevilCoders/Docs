## Что как
Утилиты для удобного грепа логов
Предполагается, что локально установлены и настроены `jq` и 
[pssh (облачный)](https://wiki.yandex-team.ru/users/landavid/pssh-documentation/) (используется по умолчанию), 
остальные команды выполняются удаленно

Опционально можно поставить [executer](https://wiki.yandex-team.ru/cloud/devel/platform-team/api-oncall/workspace/#executer) (для его использования надо перед командой написать перемнную окружения `PSSH=false `)

**Важно!** - любые утилиты по удаленному выполнению, будь то `executer` или `pssh` имеют ограничение на количество 
данных,которые они могут обработать. Это приводит к тому, что часть строчек может обрезаться, если вы выгрепываете 
слишком много. В этом случае json становится невалидным, часть информации просто отбрасывается. Поэтому **если вы хотите
проанализировать большой объем данных - используйте YT**

## Примеры
Основное, что нужно знать - скрипт чаще всего ожидает, что вы передадите ему какое-то действие, обычно - греп логов
Например:  
```
./api-gateway_access.sh "grep aoehpqtqhflgg2b4h3hc | tail -n 1"
```
или просто выполнения команды на всех инстансах:
```
./api-gateway.sh "sudo docker ps -f 'name=api-als'"
```
В случае, если команда не указана - будет выполнена дефолтная, в случае логов - это `tail -n 1`

## Для дежурного
Основные команды, которые могут помочь:
* `PROFILE=prod ./api-adapter/api-adapter_access_all.sh grep <проблемный request-id>` посмотреть 
по request_id весь путь запроса
* `PROFILE=prod ./api-gateway_access_error.sh` найти последние ошибки на api-gateway
* `PROFILE=prod ./api-adapter/api-adapter_access_long.sh` найти долгие запросы на api-adapter
* `PROFILE=prod ./api-gateway_envoy_access_long.sh` найти долгие запросы на api-gateway

## Настройка
**Важно!** - перед тем, как начинать работу с pssh - запустите pssh `pssh config -i`, чтобы он создал конфиг.

Некоторые особенности работы грепалок регулируются env-переменными
* `PROFILE` может быть `prod` или `preprod`. Если не указано - грепалка спросит об этом
* `PSSH` - если `false`, то будет выполняться executer, а не pssh. 
* `JQ_DISABLE` - отключает форматирование логов
* `JQ_TSV` - позволяет настроить вывод только нужных вам полей в табличку
* `JQ_MAP` - позволяет настроить вывод только нужных вам полей в json
* `DAY` - можно задать день, за который грепать логи. Например, `2019-04-01`. Если не указан - используется сегодняшний.
Не работает с логами java-приложений, которые ротируют логи без даты в имени файла

С остальными переменными вы обязательно столкнетесь в процессе выполнения повседневных задач
