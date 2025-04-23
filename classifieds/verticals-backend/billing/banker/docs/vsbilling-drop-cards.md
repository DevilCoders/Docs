В последнее время участились случаи мошеннеческих действий на Авто.ру, когда злоумышленники используют сайт для проверки украденных пластиковых карт при помощи механизма привязки.
Они создают новый аккаунт и привязывают к нему сотни карт, проверяя тем самым, что на них есть деньги.

Одна из типовых задач в данном случае - массовая отвязка способов оплаты одной кнопкой: вручную отвязать 700 карт не представляется возможным. Теперь у команды VSBILLING есть скрипт, который помогает делать это автоматически.

Последовательность действий такова:

1. Саппорт приходит к нам с userId подозрительного аккаунта. Для примера возьмем `71498813`.

2. `h2p banker-api-http-api`
3. Запустить в вашем любимом интерпретаторе/PyCharm'е это:
```(python)
import requests
import aiohttp
import asyncio


def collect_panmasks(uid):
    url = f"http://localhost:3000/api/1.x/service/autoru/customer/user:{uid}/method"
    res = requests.get(url, headers={'X-Vertis-User': 'autoru:salesman'})
    return [x['properties']['cddPanMask'] for x in res.json() if 'properties' in x and 'cddPanMask' in x['properties']]


async def aio_delete(uid):
    masks = collect_panmasks(user)
    print(len(masks), 'cards found')
    if (len(masks)) > 0:
        async with aiohttp.ClientSession() as session:
            for pan_mask in masks:
                pokemon_url = f"http://localhost:3000/api/1.x/service/autoru/customer/user:{uid}/method/gate/yandexkassa_v3/id/{pan_mask}"
                async with session.delete(pokemon_url, headers={'X-Vertis-User': 'autoru:salesman'}) as resp:
                    await resp.json()
    else:
        return None


user = "71498813"
asyncio.run(aio_delete(user))
```

В переменную `user` подставить userId от поддержки

Скрипт достанет все способы оплаты для данного userId, у которых есть `properties.cddPanMask` - признак привязанной банковской карты.
После чего он асинхронно удалит все из них позодом в соответствующую ручку.
Секунд через 5-10 можете повторно запустить скрипт. Ожидается, что он вернет `0 cards found`, т.е. подтвердит удаление всех привязанных карт.
