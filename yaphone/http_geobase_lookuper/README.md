# HTTP Geobase Lookuper

Обёртка над HTTP геобазой v1, имитирующая поведение объектов из geobase5

Документацию на HTTP геобазу смотрите здесь:
https://wiki.yandex-team.ru/http-geobase/api-v1/

## Установка
 `pip install yandex-http-geobase -i https://pypi.yandex-team.ru/simple/`
 
## Использование
Ранее geobase5.Lookup объект инициализировался так:
```(python)
import geobase5

geobase_lookup = geobase5.Lookup('/var/cache/geobase/geodata5.bin')
```
Заменяем его на
```(python)
import httpgeobase

geobase_lookup = httpgeobase.Lookup()
```
Опционально можно указать url, где живёт HTTP-геобаза
```(python)
geobase_lookup = httpgeobase.Lookup('https://geobase.example.com')
```

Объекты этой обёртки пытаются мимикрировать под объекты geobase5, 
за исключением некоторых методов.
