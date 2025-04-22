# Схема продакшена Директа

Актуальность: ноябрь 2020.

## Сервисы продакшена { #services }
_полноразмерную картинку можно открыть из [арканума](https://a.yandex-team.ru/arc/trunk/arcadia/direct/docs/reference/schemes/_assets/direct-production-services-202011.svg)_

Некоторые элементы схемы кликабельны: кластера (ссылки на кондуктор), балансеры (ссылки на L3—manager).  
Упрощения схемы:
- из основного nginx `direct-accel` трафик проксируется и на [другие источники](#direct-accell-proxy), на схеме показано как `...`
- разные базы данных представлены одним элементом `DB`, состав показан ниже на [отдельной схеме](#db)
- большинство приложений используют `redis_cache` — поэтому он включен в состав `DB` и [показан подробнее](#zk-redis) ниже

![production scheme](_assets/direct-production-services-202011.svg "Схема продакшена Директа")

## Проксирование трафика { #direct-accell-proxy }
Дополнительные бекенды, в которые мы проксируем трафик:
- avatars.mds.yandex.net — картинки, загруженные рекламодателями
- ad-designer.yandex.ru — интерфейс управления креативами (BannerStorage)
- lp-constructor-internal-balancer.stable.qloud-b.yandex.net — Landing Page Constructor
- help.doccenter.yandex.$tld — тултипы хелпов
- yandex.ru/promo
- yandex.ru/search/direct-preview
- passport.yandex.ru
- и другие, смотрите [конфиги](https://a.yandex-team.ru/arc/trunk/arcadia/direct/perl/etc/frontend/nginx)


## Базы данных { #db }
Уточнение представления блока `DB` из схемы сервисов.  
Подробное устройство Redis—cluster представлено [ниже](#zk-redis)

Текущую схему репликации и состояние машин показывает [Обсерваториум](https://observatorium.common.yandex.ru/storages/replication_schema).

![db scheme](_assets/direct-production-storages-202011.svg "Схема БД Директа")

## Redis и ZooKeeper { #zk-redis }
Уточнение представления блоков из схемы сервисов:
- `ZooKeeper` — хранение конфигурации, распределенные блокировки
- `redis_cache` — баллы API, распределенные блокировки
- `redis_heavy` — кеш данных с Seneca для нового интерфейса

![ppcback scheme](_assets/direct-production-zk-202011.svg "ppcback сервисы")

## Обновление схем
При актуализации схемы  нужно перегенировать картинки.
При больших обновлениях, старую схему желательно оставить для истории.

Команды для генерации (из корня docs):
```sh
dot reference/schemes/direct-production-services.dot -Tsvg -o reference/schemes/_assets/direct-production-services-`date +%Y%m`.svg
dot reference/schemes/direct-production-services.dot -Tpng -Gsize=3,3 -o reference/schemes/_assets/direct-production-services-`date +%Y%m`-preview.png
dot reference/schemes/direct-production-storages.dot -Tsvg -o reference/schemes/_assets/direct-production-storages-`date +%Y%m`.svg
dot reference/schemes/direct-production-zk.dot -Tsvg -o reference/schemes/_assets/direct-production-zk-`date +%Y%m`.svg
```

## Ссылки { #links }

- Схема репликации mysql в Обсерваториуме: <https://observatorium.common.yandex.ru/storages/replication_schema>
