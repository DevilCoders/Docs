# Masstransit matrix test shootings

Мы регулярно обстреливаем тестовый кластер рандомными запросами с синхронными и асинхронными матрицами

Таким образом мы тестируем:
* надежность сервиса
* API
* процедуру релиза под нагрузкой (так как мы работаем с распределенной базой данных, а пользовательский сценарий состоит из нескольких запросов, мы можем поймать баги, проявляющийся, когда часть запросов в пользовательской сессии приходит на обновившийся узел, а вторая - на необновившийся)


Стрелялка в большой степени списана с аналогичной автомобильной и местами используют один и тот же код.
Можно также почитать их readme [тут](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/matrix_router/quality_reporter/shooter) и [тут](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/maps/MapsMatrixRouterShootingTask).

## Планировщики в Sandbox

Код в данной папке используется внутри бинарной sandbox-таски [MapsMasstransitMtmatrixTester](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/masstransit/MapsMasstransitMtmatrixTester).

[Шедулер, запускающий стрельбы](https://sandbox.yandex-team.ru/scheduler/61193/view) - запускается раз в несколько минут.

Так как таска бинарная, нужно обновлять ее бинарник.
[Шедулер, обновляющий бинарник таски](https://sandbox.yandex-team.ru/scheduler/61317/view) - запускается ежедневно. Чтобы не ждать, можно после коммита своих изменений запустить таску вручную из этого шедулера (run once).

## Локальный запуск стрелялки

Можно использовать бинарник, собирающийся из [данной папки](https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/matrix/shooter/).

Он может стрелять без аутентификации, а также с помощью Tvm2.
Например, на тестовом кластере достаточная квота есть у пользователя maps-core-masstransit-testing-tools (tvmid:2028046).

Чтобы использовать аутентификацию по tvm2, нужно:

1. Скачать себе tvmtool [по инструкции](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/#gdeskachatbinarnik) (там же можно почитать про сам tvmtool, после чего должны стать понятнее следующие пункты).

2. Подготовить конфиг tvmtool.conf примерно такого вида:
```json
{
    "clients": {
        "maps-core-masstransit-testing-tools": {
            "secret": "<secret>",
            "self_tvm_id": 2028046,
            "dsts": {
                "s3-mds": {
                    "dst_id": 2017579
                },
                "maps-core-masstransit-matrix": {
                    "dst_id": 2025067 # masstransit matrix testing
                }
            }
        }
    },
    "port": <port>
}
```
В качестве `<secret>` либо явно указать секрет TVM-приложения maps-core-masstransit-testing-tools из [секретницы](https://yav.yandex-team.ru/secret/sec-01f5jyk087p28t19ydezkqezx2/explore/versions),
Либо написать `env:TVM_SECRET`, а секрет поместить в эту переменную окружения.

В качестве `<port>` выбрать любой незанятый порт на машине

3. Запустить tvmtool с этим конфигом:
```
./tvmtool -c tvmtool.conf
```

4. Скопировать локальный токен, который `tvmtool` пишет в лог с сообщением `Server access token`. Этот токен нужен для авторизации скрипта в локально запущен
ном `tvmtool`.

Альтернатива - сгенерить токен самому и записать его в переменную окружения `TVMTOOL_LOCAL_AUTHTOKEN`, откуда ее затем прочитают и `tvmtool`, и `shooter`.

5. Запустить скрипт стрелялки:
```
./shooter --tvmtool-port <port> [--tvmtool-auth-token <token>]
```
