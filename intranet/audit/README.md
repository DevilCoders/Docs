# audit
Сервис для Аудита

https://wiki.yandex-team.ru/Intranet/audit/

[Репозиторий фронта](https://github.yandex-team.ru/tools/audit-static)

## Разработка

Если вы начинаете разрабатывать, нужно выполнить `make first_run`.
Эта команда соберёт образ, создаст базу и доведёт её до актуального состояния.

Чтобы разрабатывать локально в дальнейшем, надо запустить `make run`

### Чтобы работал tvm локально
TVM используется в саджестах по staff (департаменты и пользователи).
При этом из коробки локально он не будет работать. Что нужно сделать, чтобы работал:

**Вариант 1**. Можно ходить в tvm-api.yandex-team.ru, но он ipv6-only. Можно настроить у себя на маке проксирование через nginx, например.

**Вариант 2**. Можно ходить получать тикеты через tvmtool:
- Установить tvmtool https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/
- Создать для него конфиг ```~/.tvm.json``` с содержимым:
```json
{
    "BbEnvType": 0,
    "clients": {
        "audit": {
            "secret": "<secret for 2000256 (взять в abc)>",
            "self_tvm_id": 2000256,
            "dsts": {
                "staff": {"dst_id": 2001976}
            }
        }
    },
    "port": 18080
}
```
>
- Запустить демона: ```tvmtool -a TOKEN_WHICH_LENGTH_IS_32_SYMBOLS -c ~/.tvm.json```
- Поставить переменные окружения:
    ```TVM2_USE_DAEMON=1```
    ```QLOUD_TVM_TOKEN=TOKEN_WHICH_LENGTH_IS_32_SYMBOLS```
    ```TVM2_API_URL=http://host.docker.internal:18080/tvm``` (хост может отличаться в зависимости от версии докера)
- После этого можно запускать docker-compose и для получения tvm он будет ходить по TVM2_API_URL

## Релиз
Нужен [releaser](https://github.yandex-team.ru/tools/releaser).

Собрать образ и выкатить на тестинг:
`releaser release`

Выкатить затем на прод:
`releaser deploy -e production`

## Тесты

`make test`
