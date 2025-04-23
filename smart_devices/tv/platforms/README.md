## Конфиг
Для заведения таргета, Таргетатору нужен конфиг, который хранится в [smart_devices/tv/platforms/\<manufacturer>/\<platform>](https://a.yandex-team.ru/arc_vcs/smart_devices/tv/platforms?rev=trunk)
Его структура следующая:
```json5
{
    "customer": "Kvant",
    "target": "LD-50SU8815BS.CC500PV5D",
    "boot_logo": "bootlogo_yandex.jpg",
    "error_logo": "boot_error.jpg",
    "recovery_logo": "boot_recovery.jpg",
    "platform": "cv9632",
    "vendorConfig": {                    //optional
        "pult": "pult_bbk",              //optional
        "banners": "banners_hi-f40",     //optional
        "feedback": "feedback_dexp"      //optional
    },
    "clids": {                           //optional
        "clid1": 2460226,
        "clid100010": 2460229,
        "clid100011": 2460227,
        "clid100012": 2460225,
        "clid100013": 2460228,
        "clid100014": 2460224
    },
    "props": {
        "brand": "Vekta",
        "name": "LD-50SU8815BS.CC500PV5D",
        "device": "LD-50SU8815BS.CC500PV5D",
        "model": "LD-50SU8815BS",
        "manufacturer": "Vekta"
    },
    "ticket": "TVANDROID-XXXX",
    "panel": "CC500PV5D"
}
```

## Ресурсы
Для заведения таргета нам нужны бутлого. Их названия ты указываешь в конфиге. Название нужного лого можно найти в папке `smart_devices/tv/platforms/resources`

## Как использовать
1. В Аркадии в директории `smart_devices/tv/platforms/<manufacturer>/<platform>` создай файл с названием `<sw_name>.json`
2. (optional) Если в `resources` нет нужных лого - добавь их
3. Смёрджи конфиг в транк
4. ???
5. Profit. В нужном репозитории создадутся пуллреквесты (или даже запустится билд прошивки в случае Stage 2)

## Больше информации
Больше информации можно найти на [Вики Таргетатора](https://wiki.yandex-team.ru/tv-android/targetator/)
