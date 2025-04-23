# Как чинить?

{% note tip %}

Если не удалось разобраться, то приходите на [горячую линию](index.md#hotline), разберёмся вместе : )

{% endnote %}

## Проблемы выкатки на сервис {#stucked-deploy}
Признаки:
1. Таймаут таски **DEPLOY_FAST_DATA**, активирующей данные (`only_prepare = False` в параметрах таски).
2. Возраст данных превысил порог.

### Залипла выкладка на определенной локации, хотя на других прокатилась {#broken-location}
Например, если данные выкатились на хамстер полностью, а на прод только в `prestable_noapache_sas_web_yp` и `production_noapache_sas_web_yp`. Следующий на очереди сервис – `production_noapache_man_web_yp`, о нем сообщения нет, значит, выкладка зависла на нем.

#### Определяем зависший под {#where-is-sick}
1. Зайти на [график возраста данных](https://nda.ya.ru/t/RBLxf5Kl3iN5wV).
2. Топ по хостам (по убыванию).
3. У залипших подов возраст будет больше чем у остальных.
4. Идём дебажить детальнее через доступные способы.

#### Первый способ {#second-pochinka}
1. Заходим на любой noapache няня-сервис (например `hamster_noapache_sas_web_yp`).
2. Необходимо понять в чём проблема. Тут помогут либо `bstr.err` либо `noapacheupper.err`.
3. Начнём с `bstr.err`. Посмотрим что сейчас происходит `tail -f bstr.err`. Если зависший in_fly, который bstr не пытается подготовить, то переходим к пункту 6. Если что-то происходит: загрузка файла, подготовка, активация, то наблюдаем и возможно процесс задержался но уже в работе.
4. Проверяем, что нет явных падений в `bstr.err`. Грепаем по нему `grep -A 10 'fail' bstr.err`. Возможно здесь будет traceback/описание от bstr сервиса с возможной причиной отказа активации сломанной fast-data.
5. Если же непонятно что там происходит. Грепаем по bstr.err `grep -E -B 10 "('prepared'|'done')" bstr.err`. Смотрим какая версия fast-data последней была подготовлена или активирована соответственно по строчке `[INFO] New data version: X` перед `[INFO] Set status ('prepared'|'done')`. Возможно этих строк вообще не будет, поэтому можно предположить что проблемы с bstr, диском либо сетью.
6. Переводим больной под в PREPARED и делаем eviction ему либо исследуем и активируем вновь.
7. Если ошибка всё равно непонятна, то возможно будет видно в `noapacheupper.err`. Здесь грепаем `grep -A 3 i 'error'` и смотрим на что ругается noapache.

#### Второй способ {#third-pochinka}
1. Найти работающий (взявший лок на выкладку) инстанс в сервисе [noapache_fast_data_deployer_web](https://nanny.yandex-team.ru/ui/#/services/catalog/noapache_fast_data_deployer_web/). Для этого запустить ` tail -f deployer.err` – работающий инстанс постоянно пишет статус выкладки.
2. В директории с логами `/logs` найти лог про нужный сервис, вывести его: `tail -n 10000 production_noapache_man_web_yp.prepare.log` (или можно посмотреть в `deployer.err`).
3. Находим строчку `Retry preparing \<N\> instances`, дальше идет список инстансов, на которые не удается выложить данные.
4. Пробуем понять, почему не получается выложить данные туда. Если не получается, то заказываем для пода eviction или переводим в PREPARED.

### Не катается **НИГДЕ** {#broken-all}
Обычно это случается когда какой-то коммит ломает noapache, из-за чего он не может подняться с текущей (сломанной) fast-data. Но возможны и другие причины. В любом случае:

1. Заходим на любой noapache няня-сервис (например `hamster_noapache_sas_web_yp`).
2. Необходимо понять в чём проблема. Тут помогут либо `bstr.err` либо `noapacheupper.err`.
3. Начнём с `bstr.err`. Грепаем по нему `grep -A 10 'fail' bstr.err`. Здесь будет traceback/описание от bstr сервиса с возможной причиной отказа активации сломанной fast-data.
4. Если ошибка всё равно непонятна, то обращаемся к `noapacheupper.err`. Здесь грепаем `grep -A 3 i 'error'` и смотрим на что ругается noapache.

## Ошибка выкладки данных на бету {#beta-deploy-fail}
Признаки:
1. Таймаут/failure таски **DEPLOY_FAST_DATA** с родительской таской **TEST_REARRANGE_DATA_FAST_ON_YAPPY_BETA**.
2. Failure **TEST_REARRANGE_DATA_FAST_ON_YAPPY_BETA** с текстом по типу `Incorrect fast data version on noapacheupper-priemka-2-yp-3.vla.yp-c.yandex.net:80: v.44704 deployed, v.44702 read`.

Что нужно сделать:
- Используя [инструкцию](#stucked-deploy) определить причину нерабочей выкатки. Если не получается - используем остальные рекомендации.
- Посмотреть в логи `deployer.err`: `DEPLOY_FAST_DATA` -> `log1` -> `deployer.err.log`. Посмотреть, на чем deployer завис/пофейлился.
- Зайти в бету [Yappy](https://yappy.z.yandex-team.ru/b/noapache-web-fast-data/components), посмотреть нет ли там каких проблем.
- Если проблема с няня сервисом в бете, то может помочь "поменяться" сервисами с основной квотой ноапача в Yappy. Для этого нужно поменять списки сервисов тут: [noapache@noapacheupper](https://yappy.z.yandex-team.ru/q/noapache@noapacheupper/json), [noapache@noapacheupper-web-fastdata](https://yappy.z.yandex-team.ru/q/noapache@noapacheupper-web-fastdata/json).