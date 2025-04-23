# rasp-proto-schemas

В пакете собранны схемы расписаний в protobuf формате.
Все схемы выкачиваются из [аркадии](https://a.yandex-team.ru/arc/trunk/arcadia/travel/rasp/pathfinder_maps/maps_protos).

## Установка

```
npm install @yandex-int/maps-proto-schemas
```

## Обновления схем

Для обновления схем на свежую версию из аркадии необходимо выполнить команду:
```
    npm run update-revision
    npm run build
```

## Сборка

Чтобы пересобрать текущую версию схем, указанную в файле [revision](revision), выполните:
```npm run build```

## Публикация пакета

```npm publish```
