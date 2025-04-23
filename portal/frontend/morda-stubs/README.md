# yandex-lg-tv-www

Это заглушки для старых тв и девайсоспецифичных морд
 - hw.yandex.ru/lg
 - hw.yandex.ru/lg-v2
 - hw.yandex.ru/op
 - hw.yandex.ru/ph
 - hw.yandex.ru/bmw
 - op.yandex.ru
 
Для разработки не нужен бэкенд, достаточно сконфигурировать:
`npm run conf`

Либо запустить дебаг-сервер локально:
`npm run debug`

морды будут доступны по адресам
```
lg-<инстанс>.wdevx.yandex.ru/lg
op-<инстанс>.wdevx.yandex.ru
```

## Как релизить

1. `npm run release`
2. проверить в тестинге (hw-test.yandex.ru, op-test.yandex.ru)
3. выкатить в прод

Подробнее [на вики](https://wiki.yandex-team.ru/morda/hwyandexnet/#zaglushkitvmord)
