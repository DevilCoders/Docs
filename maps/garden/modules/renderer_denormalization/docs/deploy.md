# Сборка и деплой renderer_denormalization

## Локальная сборка модуля

```
ya make -r maps/garden/modules/renderer_denormalization/bin
```

## Деплой модуля в песочницу

Огородная инструкция: https://docs.yandex-team.ru/garden/experiments

## Деплой модуля в тестинг

Огородная инструкция: https://docs.yandex-team.ru/garden/module-lifecycle#sedem
Релизы в Sedem: https://docs.yandex-team.ru/sedem/releases

Зарелизить `r1234567` в testing:
```
ya tool sedem release start maps/garden/modules/renderer_denormalization r1234567
```

## Создание hotfix

Инструкция Sedem: https://docs.yandex-team.ru/sedem/releases#release-hotfix

Коммитим исправления в trunk (`r456123`):
```
$ svn commit -m "Fix something REVIEW:NEW"
...
Committed revision 456123.
```

Узнаем номер ветки в нужном стейджинге (`v135`):
```
$ ya tool sedem release info maps/garden/modules/renderer_denormalization
...
│ testing │ 5 days ago │ v135.1    │ MAPSRELEASES-12345 │ commit message │
...
```

Делаем hotfix в ветку `v135` с исправлением `r456123` из trunk:
```
$ ya tool sedem release hotfix maps/garden/modules/renderer_denormalization -b v135 -r r456123
```

Если в результате наложения хотфикса возникли мердж конфликты, их нужно разрешить вручную:
```
$ ya clone --branch=branches/maps-releases/maps_garden_renderer_denormalization-135 hotfix-135
$ cd hotfix-135
$ svn update --set-depth infinity maps
$ svn merge -c 456123 svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia
разрешаем конфликт
$ svn commit -m "Merge revision 456123 into hotfix SKIP_REVIEW SKIP_CHECK"
```
Подождать пока CI соберет модуль (`v135.1` -> `v135.2`), зарелизить модуль в нужный стейджинг:
```
$ ya tool sedem release step maps/garden/modules/renderer_denormalization v135.2 testing
```
