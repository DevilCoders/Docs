# Схема продакшена Директа

Актуальность: август 2021.

## Сервисы продакшена { #services }
_полноразмерную картинку можно открыть из [арканума](https://a.yandex-team.ru/arc/trunk/arcadia/direct/docs/reference/schemes/_assets/direct-production-services-202108.svg)_

Некоторые элементы схемы кликабельны: кластера (ссылки на кондуктор), балансеры (ссылки на L3—manager).  
Упрощения схемы:
- из основного nginx `direct-accel` трафик проксируется и на [другие источники](#direct-accell-proxy), на схеме показано как `...`
- разные базы данных представлены одним элементом `DB`, состав показан ниже на [отдельной схеме](#db)
- большинство приложений используют `redis_cache` — поэтому он включен в состав `DB` и [показан подробнее](#zk-redis) ниже

Также на схеме не показан UAC (живет немного сбоку директа, но ходит в наше интапи) и DNA (jsки, лежат на перловых фронтах).

![production scheme](_assets/direct-production-services-202108.svg "Схема продакшена Директа")

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
Уточнение представления блока `DB` из схемы сервисов. Оно включает в себя следущие хранилища в MDB:
- 21 шард MySQL базы **ppc** x 3ДЦ
- MySQL база **ppcdict** x 3ДЦ
- MySQL база **monitor** x 3ДЦ
- **redis_cache** — баллы API, распределенные блокировки (9 нод в 3ДЦ)
- **redis_heavy** — кеш данных с Seneca для нового интерфейса (9 нод в 3ДЦ)

Текущую схему репликации MySQL и состояние машин показывает [Обсерваториум](https://observatorium.common.yandex.ru/storages/replication_schema).

## ZooKeeper { #zk }
Еще есть собственный кластер Zookeeper, используемый для хранение конфигурации и распределенных блокировок.

![ZK scheme](_assets/direct-production-zk-202108.svg "ZooKeeper")

## Обновление схем
При актуализации схемы  нужно перегенировать картинки.
При больших обновлениях, старую схему желательно оставить для истории.

Команды для генерации (из корня docs):
```sh
dot reference/schemes/direct-production-services.dot -Tsvg -o reference/schemes/_assets/direct-production-services-`date +%Y%m`.svg
dot reference/schemes/direct-production-services.dot -Tpng -Gsize=3,3 -o reference/schemes/_assets/direct-production-services-`date +%Y%m`-preview.png
dot reference/schemes/direct-production-zk.dot -Tsvg -o reference/schemes/_assets/direct-production-zk-`date +%Y%m`.svg
```

## Ссылки { #links }

- Схема репликации mysql в Обсерваториуме: <https://observatorium.common.yandex.ru/storages/replication_schema>
