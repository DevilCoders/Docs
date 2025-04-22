---
title: cfg_tool
---
## cfg_tool - Что это?
Тулза для заливки конфигов, хранящихся в Аркадии, в YT для дальнейшего использования в сервисах.
В данный момент есть такие конфиги:
* Списки операторов и партнёров [тут](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/config/cfg_tool/partners_and_operators.config)
* Список клиентов офферкэша [тут](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/config/cfg_tool/offercache_clients.config)
* Черный и белый списки отелей [тут](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/config/cfg_tool/hotel_lists.config)
* И многое другое

## Иерархия конфигов
Конфиги читаются из указанных выше файлов, при этом в файлах с суффиксами `-testing` и `-prod` находятся "уточняющие" конфиги, специфичные для окружения

## Куда оно кладётся на YT ?
* [Prod](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod/config)
* [Testing](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/testing/config)

## Использование
Для изменения конфига - нужно поправить соответствующий файл, далее можноо запустить валидацию через `ya make -t` в директории `travel/hotels/devops/cfg_tool`.

Для заливки конфигов в тестинг и прод надо закоммитить изменения. Далее отработает автоматика, и изменения будут залиты сначала в тестинг, а потом в прод.
Оповещения о ходе заливки можно увидеть в Slack, в канале #понябот-build-notifications.

## А если я хочу что-то изменить только в тестинге?
Заводите файл с суффиксом `-testing`.

## Как выключить оператора в проде?
В [файле](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/config/cfg_tool/partners_and_operators-prod.config) написать
```
Operator {
    OperatorId: OI_<оператор>; Enabled: false;
}
```

и закоммитить файл

## Как добавить отель в WL в проде?
В [файле](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/config/cfg_tool/hotel_lists-prod.config) написать
```
WhitelistedHotel { Permalink: ...; PartnerId: PI_...; OriginalId: "..."; }
```

и закоммитить файл

## Как забанить отель в проде?
В [файле](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/config/cfg_tool/hotel_lists-prod.config) написать
```
BlacklistedHotel { Permalink: ...; PartnerId: PI_...; OriginalId: "..."; }
```

и закоммитить файл
