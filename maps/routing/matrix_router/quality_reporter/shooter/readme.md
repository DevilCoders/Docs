Этот код используется внутри бинарной Sandbox-таски
[MapsMatrixRouterShootingTask](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/maps/MapsMatrixRouterShootingTask).
Более подробное описание там.

Таска регулярно запускается,
[посмотреть список запусков можно здесь](https://sandbox.yandex-team.ru/scheduler/43483/view).

**После коммита в этот код рекомендуется сразу загрузить новую версию таски, вручную запустив
[соответствующий планировщик](https://sandbox.yandex-team.ru/scheduler/43940/view).** Раз в
сутки он запускается автоматически.


# Как использовать TVM

1. Установить `tvmtool`. Например, через питоновский пакет:
```
pip install tvmtool-bin -i https://pypi.yandex-team.ru/simple
```
Другие способы установки (например, через дебиановские пакеты) есть в
[документации](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/#kakzapustittvm-demona).

2. Создать конфиг `~/.tvm.json`:
```json
{
    "clients": {
        "matrix-router-testing-tools": {
            "self_tvm_id": 2026692,
            "secret": "<secret>",
            "dsts": {
                "matrix-router-testing": {
                    "dst_id": 2017359
                },
                "mds-stable": {
                    "dst_id": 2000273
                }
            }
        }
    }
}
```
В качестве `<secret>` указать секрет TVM-приложения "Automated Testing Tools"
[из секретницы](https://yav.yandex-team.ru/secret/sec-01ezyz2318pdsm44tk6qzb4zxg).
Для доступа к этому секрету нужно запросить роль "TVM менеджер" в
[сервисе матричного роутера](https://abc.yandex-team.ru/services/maps-core-matrix-router).

3. Запустить `tvmtool` на свободном порту (что-то вроде `12345`, скорее всего,
подойдёт):
```
tvmtool --port <port>
```

4. Скопировать локальный токен, который `tvmtool` пишет в лог, с сообщением
`Server access token`. Этот токен нужен для авторизации скрипта перед локально
запущенным `tvmtool`.

5. Запустить скрипт:
```
    ./shooter --tvmtool-port <port> --tvmtool-auth-token <token>
```
где `<token>` это локальный токен из лога в пункте (3).

Если `--tvmtool-port` не указан, подразумевается порт `1`.

Если `--tvmtool-auth-token` не указан, токен ищется в переменной окружения
`TVMTOOL_LOCAL_AUTHTOKEN`, а затем в файле `/var/lib/tvmtool/local.auth`. Если
`tvmtool` установлен из дебиановского пакета, он автоматически записывает
локальный токен в этот файл.

Отключить использование TVM можно с помощью ключа `--no-tvm`.
