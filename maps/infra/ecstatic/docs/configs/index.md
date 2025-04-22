Сейчас вся документация лежит [тут](https://wiki.yandex-team.ru/maps/dev/core/ecstatic/)

### Switch in parallel { #switch-in-parallel }

Switch in parallel позволяет избежать синхронного переключения данных на всем кластере. Гарантируется, что в каждый момент времени выполняется не более switch in parallel хуков. 

#### Синтаксис:
```
switch 10% of rtc:maps_core_teapot_stable in parallel
```

Вместо `10%` можно указать количество хостов, например ``switch 1 of rtc:maps_core_teapot_stable in parallel``. 

Также, есть возможность указывать более сложные конструкции, например ``switch 100% - 1 of rtc:maps_core_teapot_stable in parallel``. При таком конфиге одновременно смогут переключаться все хосты кроме 1.

Также, есть поддержка переключений данных по дц. Для этого надо написать в конфиги ``switch dc max 25% of rtc:maps_core_teapot_stable in parallel``. При таком конфиге одновременно будет переключаться не более 25% кластера и все переключающиеся машинки будут в 1 дц.

### Tolerance { #tolerance }

TODO

### Preserved data { #preserved-data }

TODO

### Ретраи хуков { #retries }

TODO
