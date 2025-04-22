## Что тут происходит
Данная инструкция предназначена в первую очередь для дежурного релизного инженера бэкенд-сервисов Народной Карты. Для обычного выкатывания в тестинг как правило достаточно [основной инструкции к sedem release](https://docs.yandex-team.ru/sedem/releases) и иногда пунктов про [миграции](#migrations) и [права](#permissions).

## Что нужно знать перед любым выкатыванием

**Прежде всего, будет очень хорошо прочитать [основную инструкцию к sedem release](https://docs.yandex-team.ru/sedem/releases)**  
**Если в процессе выкатывания вам стало ~~плохо~~ничего не понятно, возникли непреодолимые трудности, то нужно обращаться в чат maps-wiki-dev.** Там помогут. Если там вдруг не помогут, есть ещё Geo Helpline.<a name="sos"></a>
Эта инструкция про то, как катить сервисы Народной Карты с помощью Седема. Начнём с того, откуда собственно брать Седем. Самый правильный способ - брать бинарь, доступный в ya, то есть `ya tool sedem`. Учитывая, что Седем активно разрабатывается, лучше всего брать версию ya из свежего транка, он будет подтягивать самую свежую версию Седема. Я рекомендую сделать алиас в bashrc (whatevershrc) вида `alias sedem='~/arcadia/ya tool sedem'` и заниматься выкатыванием на свежем транке.


### Небольшой чеклист для самопроверки перед выкатыванием: <a name="checklist"></a>

Чеклист предлагается проходить перед любыми действиями с релизами.

1. Свежий транк
   1) Если arc: `arc checkout trunk; arc pull`
   2) Если svn: ~~переехать на arc~~ `svn up ya; svn up maps/wikimap/mapspro/services` (как минимум)
2. Рабочая директория выкладок `maps/wikimap/mapspro/services`.
3. Седем работает и версия достаточно свежая:
   ```
   chikunov@maps-nmaps-dev:~/arc/arcadia/maps/wikimap/mapspro/services$ sedem --version
   SEDEM, version xxxxxx
   ```


### Нужно также иметь в виду следующий ряд моментов:

* Под тестингом и стейблом здесь в основном понимаются стейджинги всей Народной Карты. В рамках тестинга может быть несколько стейджингов отдельного сервиса. Например, у editor/reader есть unstable, testing и load, которые катятся параллельно одной командой, а у editor/writer есть только testing.
* Для редактора нужно катить два сервиса: editor/reader и editor/writer. Ревизии должны быть одинаковые в рамках каждого отдельно взятого стейджинга.
* Путь к серванту tasks относительно рабочей директории менее очевиден, чем у остальных сервисов: tasks/fastcgi.
* tasks_misc и tasks_export не активируются в стейбле сами и требуют ручного подтверждения в Няне. При этом нужно убедиться, что нет запущенных очень длинных задач, иначе выкладка может их убить. Для [tasks_misc](#tasksmiscconfirm) это импорт, подготовка релизной ветки, синхронизация представлений, групповое редактирование. Для [tasks_export](#tasksexportconfirm) это экспорт и пакетный экспорт.
* Процедура открытия тестинга подразумевает его обновление/выкатку. После выкатывания стейбла тестинг остаётся закрытым (состояние тестинга связано с состоянием стейбла) и его нужно как можно быстрее открыть, чтобы любой разработчик мог свободно выкатывать свои изменения без оглядки на изменения других разработчиков.

## Этапы выкатывания релиза в стейбл релизным инженером

Здесь краткая последовательность действий для релизного инженера. Подробное объяснение, как выполнять отдельные пункты, последует ниже.  
Важно: **задержки между этапами не приветствуются.**
1. Получить отмашку на выкатывание (Сообщение в телеграме от confeta@ вида "мы готовы к релизу")
2. Выкатить сервис maintenance в стейбл.
3. Накатить миграции в стейбле.
4. Обновить пермишоны в стейбле.
5. [Выкатить остальные сервисы в стейбл](#vykladkavsexostalnyxservisovvstejjbl).
6. [Вручную подтвердить выкладку некоторых сервисов](#ruchnoepodtverzhdenievnanny).
7. Поглядывать на [дашборд стейбла](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_nmaps_stable/) или [инфру](https://infra.yandex-team.ru/timeline?preset=Gj1ZDUJyF8J) и, когда всё докатится (кроме, возможно, tasks_export), ответить на отмашку, что бэкенд выкатился.
8. Выкатить самую свежую версию maintenance в тестинг.
9. Накатить миграции в тестинге и анстейбле.
10. Выкатить остальной софт в тестинг. Для тестинга никакие сервисы не требуют подтверждения в nanny.
11. **Не забыть про подтверждение активации требуемых сервисов в stable**.


## Стейбл

### Выкладка maintenance в стейбл

1. Проходим [чеклист](#checklist) самопроверки перед выкатыванием.
2. Произносим в командной строке заклинание `sedem release info maintenance`. На выходе должно быть что-то вроде
   ```
   Loading service state........
   ┌ Service maps-core-nmaps-maintenance ─────────────────┬────────────────────────────────────────────────────────────────────────────────┐
   │          │ Released   │ Version │ St ticket          │ Comment                                                                        │
   ├──────────┼────────────┼─────────┼────────────────────┼────────────────────────────────────────────────────────────────────────────────┤
   │   stable │ 5 days ago │ v160.1  │ MAPSRELEASES-12849 │ (@ponomarev) NMAPS-14390 lib social: speedup filter by created-by, modified-by │
   ├──────────┼────────────┼─────────┼────────────────────┼────────────────────────────────────────────────────────────────────────────────┤
   │  testing │ 5 days ago │ v161.1  │ MAPSRELEASES-12948 │ (@mr-spock) User position quality                                              │
   │ unstable │ 5 days ago │ v161.1  │ MAPSRELEASES-12948 │ (@mr-spock) User position quality                                              │
   └──────────┴────────────┴─────────┴────────────────────┴────────────────────────────────────────────────────────────────────────────────┘
   ┌ Deploy (step) candidates ─────────────────┬───────────────────────────────────┐
   │ Version │ Created    │ St ticket          │ Comment                           │
   ├─────────┼────────────┼────────────────────┼───────────────────────────────────┤
   │  v161.1 │ 5 days ago │ MAPSRELEASES-12948 │ (@mr-spock) User position quality │
   └─────────┴────────────┴────────────────────┴───────────────────────────────────┘
   ┌ Release (start) candidates ────────┬───────────────────────────────────────────────────────────────────┐
   │  Version │ Created    │ Sb task    │ Comment                                                           │
   ├──────────┼────────────┼────────────┼───────────────────────────────────────────────────────────────────┤
   │ r8737055 │ 3 days ago │ 1101275489 │ (@euclid) NMAPS-14420 add point geometry to image_overlay/public. │
   └──────────┴────────────┴────────────┴───────────────────────────────────────────────────────────────────┘
   ```
3. Убеждаемся, что стейбл отстаёт от тестинга (`V160.1` < `V161.1`). Если не отстаёт, значит миграции в текущем релизе не менялись. Если это не так, нужно разобраться, правильная ли версия в стейбле и почему так произошло.
4. Запускаем релиз заклинанием `sedem release step maintenance <version> stable`, где `<version>` - текущая версия в тестинге. В нашем примере мы катим версию V161.1, поэтому заклинание превратится в `sedem release step maintenance V161.1 stable`.

### Выкладка всех остальных сервисов в стейбл <a name="vykladkavsexostalnyxservisovvstejjbl"></a>

1. Проходим [чеклист](#checklist) самопроверки перед выкатыванием.
2. Проверяем дифф между стейблом и тестингом:
   ```
   chikunov@maps-nmaps-dev:~/arc/arcadia/maps/wikimap/mapspro/services$ sedem release info nmaps
   Loading service state.............................................................................................................................
   ┌ Meta-service maps-core-nmaps ─────┬────────────┬─────────┬────────────────────┬──────────────────────────────────────────────────────────────────────────────────────────────────┐
   │                    Stable release │ Released   │ Version │ ST Ticket          │ Comment                                                                                          │
   ├───────────────────────────────────┼────────────┼─────────┼────────────────────┼──────────────────────────────────────────────────────────────────────────────────────────────────┤
   │               maps-core-nmaps-acl │ 5 days ago │ v125.1  │ MAPSRELEASES-12802 │ (@khrolenko) GEOINFRA-2877 move wikimap to new secret configuration scheme                       │
   ├───────────────────────────────────┼────────────┼─────────┼────────────────────┼──────────────────────────────────────────────────────────────────────────────────────────────────┤
   │  maps-core-nmaps-dataset-explorer │ 5 days ago │ v49.1   │ MAPSRELEASES-12793 │ (@khrolenko) GEOINFRA-2877 move wikimap to new secret configuration scheme                       │
   ├───────────────────────────────────┼────────────┼─────────┼────────────────────┼──────────────────────────────────────────────────────────────────────────────────────────────────┤
   │            maps-core-nmaps-editor │ 5 days ago │ v223.1  │ MAPSRELEASES-12821 │ (@euclid) New design                                                                             │
   ├───────────────────────────────────┼────────────┼─────────┼────────────────────┼──────────────────────────────────────────────────────────────────────────────────────────────────┤
   │     maps-core-nmaps-editor-writer │ 5 days ago │ v223.1  │ MAPSRELEASES-12825 │ (@euclid) New design                                                                             │
   ├───────────────────────────────────┼────────────┼─────────┼────────────────────┼──────────────────────────────────────────────────────────────────────────────────────────────────┤
   │              maps-core-nmaps-gdpr │ a week ago │ v36.1   │ MAPSRELEASES-12528 │ (@robot-maps-sandbox) Update base image version: to 8672302                                      │
   ├───────────────────────────────────┼────────────┼─────────┼────────────────────┼──────────────────────────────────────────────────────────────────────────────────────────────────┤
   │           maps-core-nmaps-grinder │ 5 days ago │ v73.1   │ MAPSRELEASES-12519 │ (@chikunov) maps-grinder-worker: remove unnecessary include                                      │
   ├───────────────────────────────────┼────────────┼─────────┼────────────────────┼──────────────────────────────────────────────────────────────────────────────────────────────────┤
   │    maps-core-nmaps-renderer-nmaps │ 5 days ago │ v96.1   │ MAPSRELEASES-12823 │ (@euclid) New design                                                                             │
   ├───────────────────────────────────┼────────────┼─────────┼────────────────────┼──────────────────────────────────────────────────────────────────────────────────────────────────┤
   │  maps-core-nmaps-renderer-overlay │ a week ago │ v58.1   │ MAPSRELEASES-12521 │ (@robot-maps-sandbox) Update base image version: to 8672302                                      │
   ├───────────────────────────────────┼────────────┼─────────┼────────────────────┼──────────────────────────────────────────────────────────────────────────────────────────────────┤
   │            maps-core-nmaps-social │ 5 days ago │ v187.1  │ MAPSRELEASES-12855 │ (@ponomarev) NMAPS-14390 magic again                                                             │
   ├───────────────────────────────────┼────────────┼─────────┼────────────────────┼──────────────────────────────────────────────────────────────────────────────────────────────────┤
   │ maps-core-nmaps-social-backoffice │ 5 days ago │ v57.1   │ MAPSRELEASES-12847 │ (@ponomarev) NMAPS-14390 lib social: speedup filter by created-by, modified-by                   │
   ├───────────────────────────────────┼────────────┼─────────┼────────────────────┼──────────────────────────────────────────────────────────────────────────────────────────────────┤
   │             maps-core-nmaps-tasks │ 5 days ago │ v76.1   │ MAPSRELEASES-12796 │ (@khrolenko) GEOINFRA-2877 move wikimap to new secret configuration scheme                       │
   ├───────────────────────────────────┼────────────┼─────────┼────────────────────┼──────────────────────────────────────────────────────────────────────────────────────────────────┤
   │      maps-core-nmaps-tasks-export │ 5 days ago │ v160.1  │ MAPSRELEASES-12798 │ (@ponomarev) NMAPS-14351 poi_auto,poi_leisure with indoor_plan                                   │
   ├───────────────────────────────────┼────────────┼─────────┼────────────────────┼──────────────────────────────────────────────────────────────────────────────────────────────────┤
   │    maps-core-nmaps-tasks-feedback │ 5 days ago │ v143.2  │ MAPSRELEASES-12803 │ (@miror) NMAPS-14391-collect-geometry-from-uri                                                   │
   ├───────────────────────────────────┼────────────┼─────────┼────────────────────┼──────────────────────────────────────────────────────────────────────────────────────────────────┤
   │        maps-core-nmaps-tasks-misc │ 5 days ago │ v125.1  │ MAPSRELEASES-12824 │ (@euclid) New design                                                                             │
   ├───────────────────────────────────┼────────────┼─────────┼────────────────────┼──────────────────────────────────────────────────────────────────────────────────────────────────┤
   │    maps-core-nmaps-tasks-realtime │ 5 days ago │ v158.1  │ MAPSRELEASES-12822 │ (@euclid) New design                                                                             │
   ├───────────────────────────────────┼────────────┼─────────┼────────────────────┼──────────────────────────────────────────────────────────────────────────────────────────────────┤
   │      maps-core-nmaps-tasks-social │ 5 days ago │ v106.1  │ MAPSRELEASES-12799 │ (@vbystricky) Добавил вариант описания гипотезы в случае если не найден знак отвественный за ... │
   ├───────────────────────────────────┼────────────┼─────────┼────────────────────┼──────────────────────────────────────────────────────────────────────────────────────────────────┤
   │       maps-core-nmaps-tasks-sprav │ 4 days ago │ v153.2  │ MAPSRELEASES-12820 │ (@euclid) GEOMONITORINGS-17132 Fix typo                                                          │
   ├───────────────────────────────────┼────────────┼─────────┼────────────────────┼──────────────────────────────────────────────────────────────────────────────────────────────────┤
   │          maps-core-nmaps-tasks-yt │ 5 days ago │ v147.1  │ MAPSRELEASES-12805 │ (@ponomarev) NMAPS-14351 poi_auto,poi_leisure with indoor_plan                                   │
   └───────────────────────────────────┴────────────┴─────────┴────────────────────┴──────────────────────────────────────────────────────────────────────────────────────────────────┘
   ┌ Meta-release candidate ───────────┬─────────────┬─────────┬────────────────────┬────────────────────────────────────────────────────────────────────────────┐
   │                   Testing release │ Released    │ Version │ ST Ticket          │ Comment                                                                    │
   ├───────────────────────────────────┼─────────────┼─────────┼────────────────────┼────────────────────────────────────────────────────────────────────────────┤
   │               maps-core-nmaps-acl │ 5 days ago  │ v126.1  │ MAPSRELEASES-12951 │ (@mr-spock) User position quality                                          │
   ├───────────────────────────────────┼─────────────┼─────────┼────────────────────┼────────────────────────────────────────────────────────────────────────────┤
   │  maps-core-nmaps-dataset-explorer │ a week ago  │ v49.1   │ MAPSRELEASES-12793 │ (@khrolenko) GEOINFRA-2877 move wikimap to new secret configuration scheme │
   ├───────────────────────────────────┼─────────────┼─────────┼────────────────────┼────────────────────────────────────────────────────────────────────────────┤
   │            maps-core-nmaps-editor │ an hour ago │ v225.3  │ MAPSRELEASES-13009 │ (@euclid) NMAPS-14387 acl user by login fixes                              │
   ├───────────────────────────────────┼─────────────┼─────────┼────────────────────┼────────────────────────────────────────────────────────────────────────────┤
   │     maps-core-nmaps-editor-writer │ an hour ago │ v225.3  │ MAPSRELEASES-13014 │ (@euclid) NMAPS-14387 acl user by login fixes                              │
   ├───────────────────────────────────┼─────────────┼─────────┼────────────────────┼────────────────────────────────────────────────────────────────────────────┤
   │              maps-core-nmaps-gdpr │ 5 days ago  │ v37.1   │ MAPSRELEASES-12963 │ (@euclid) NMAPS-14268 Add delete reason for acl users                      │
   ├───────────────────────────────────┼─────────────┼─────────┼────────────────────┼────────────────────────────────────────────────────────────────────────────┤
   │           maps-core-nmaps-grinder │ 5 days ago  │ v74.1   │ MAPSRELEASES-12955 │ (@naplavkov) mrc-grinder: sedem_config/secrets.yaml                        │
   ├───────────────────────────────────┼─────────────┼─────────┼────────────────────┼────────────────────────────────────────────────────────────────────────────┤
   │    maps-core-nmaps-renderer-nmaps │ 3 hours ago │ v97.2   │ MAPSRELEASES-13011 │ (@euclid) Design NMAPSDESIGN-120 +  hot fix.                               │
   ├───────────────────────────────────┼─────────────┼─────────┼────────────────────┼────────────────────────────────────────────────────────────────────────────┤
   │  maps-core-nmaps-renderer-overlay │ 2 weeks ago │ v58.1   │ MAPSRELEASES-12521 │ (@robot-maps-sandbox) Update base image version: to 8672302                │
   ├───────────────────────────────────┼─────────────┼─────────┼────────────────────┼────────────────────────────────────────────────────────────────────────────┤
   │            maps-core-nmaps-social │ 4 days ago  │ v189.1  │ MAPSRELEASES-13015 │ (@mr-spock) POI location editor configs                                    │
   ├───────────────────────────────────┼─────────────┼─────────┼────────────────────┼────────────────────────────────────────────────────────────────────────────┤
   │ maps-core-nmaps-social-backoffice │ 5 days ago  │ v58.1   │ MAPSRELEASES-12961 │ (@ponomarev) NMAPS-14390 magic again                                       │
   ├───────────────────────────────────┼─────────────┼─────────┼────────────────────┼────────────────────────────────────────────────────────────────────────────┤
   │             maps-core-nmaps-tasks │ 5 days ago  │ v77.1   │ MAPSRELEASES-12950 │ (@khrolenko) more strict balancer conf for maps                            │
   ├───────────────────────────────────┼─────────────┼─────────┼────────────────────┼────────────────────────────────────────────────────────────────────────────┤
   │      maps-core-nmaps-tasks-export │ 3 days ago  │ v163.1  │ MAPSRELEASES-13036 │ (@mr-spock) New POI location export                                        │
   ├───────────────────────────────────┼─────────────┼─────────┼────────────────────┼────────────────────────────────────────────────────────────────────────────┤
   │    maps-core-nmaps-tasks-feedback │ 5 days ago  │ v144.1  │ MAPSRELEASES-12957 │ (@miror) NMAPS-14391-collect-geometry-from-uri                             │
   ├───────────────────────────────────┼─────────────┼─────────┼────────────────────┼────────────────────────────────────────────────────────────────────────────┤
   │        maps-core-nmaps-tasks-misc │ 3 days ago  │ v128.1  │ MAPSRELEASES-13035 │ (@euclid) NMAPS-14426 Design update                                        │
   ├───────────────────────────────────┼─────────────┼─────────┼────────────────────┼────────────────────────────────────────────────────────────────────────────┤
   │    maps-core-nmaps-tasks-realtime │ 3 days ago  │ v161.1  │ MAPSRELEASES-13034 │ (@euclid) NMAPS-14426 Design update                                        │
   ├───────────────────────────────────┼─────────────┼─────────┼────────────────────┼────────────────────────────────────────────────────────────────────────────┤
   │      maps-core-nmaps-tasks-social │ 5 days ago  │ v107.1  │ MAPSRELEASES-12962 │ (@ponomarev) NMAPS-14390 magic again                                       │
   ├───────────────────────────────────┼─────────────┼─────────┼────────────────────┼────────────────────────────────────────────────────────────────────────────┤
   │       maps-core-nmaps-tasks-sprav │ 3 days ago  │ v156.1  │ MAPSRELEASES-13033 │ (@mr-spock) New POI location export                                        │
   ├───────────────────────────────────┼─────────────┼─────────┼────────────────────┼────────────────────────────────────────────────────────────────────────────┤
   │          maps-core-nmaps-tasks-yt │ 4 days ago  │ v149.1  │ MAPSRELEASES-13010 │ (@mr-spock) POI location editor configs                                    │
   └───────────────────────────────────┴─────────────┴─────────┴────────────────────┴────────────────────────────────────────────────────────────────────────────┘
   ```
3. Если нет аномалий, то катим: `sedem release step nmaps V1 stable`. V1 здесь не несёт никакого смысла и нужно только для соответствия порядку аргументов.


## Тестинг

### Выкладка сервисов в тестинг

1. Проходим [чеклист](#checklist) самопроверки перед выкатыванием.
2. Произносим в командной строке заклинание `sedem release info <service-path>`. <service-path> - путь к сервису относительно рабочей директории. На выходе должно быть что-то вроде
   ```
   chikunov@maps-nmaps-dev:~/arc/arcadia/maps/wikimap/mapspro/services$ sedem release info maintenance
   Loading service state........
   ┌ Service maps-core-nmaps-maintenance ─────────────────┬────────────────────────────────────────────────────────────────────────────────┐
   │          │ Released   │ Version │ St ticket          │ Comment                                                                        │
   ├──────────┼────────────┼─────────┼────────────────────┼────────────────────────────────────────────────────────────────────────────────┤
   │   stable │ 5 days ago │ v160.1  │ MAPSRELEASES-12849 │ (@ponomarev) NMAPS-14390 lib social: speedup filter by created-by, modified-by │
   ├──────────┼────────────┼─────────┼────────────────────┼────────────────────────────────────────────────────────────────────────────────┤
   │  testing │ 5 days ago │ v161.1  │ MAPSRELEASES-12948 │ (@mr-spock) User position quality                                              │
   │ unstable │ 5 days ago │ v161.1  │ MAPSRELEASES-12948 │ (@mr-spock) User position quality                                              │
   └──────────┴────────────┴─────────┴────────────────────┴────────────────────────────────────────────────────────────────────────────────┘
   ┌ Deploy (step) candidates ─────────────────┬───────────────────────────────────┐
   │ Version │ Created    │ St ticket          │ Comment                           │
   ├─────────┼────────────┼────────────────────┼───────────────────────────────────┤
   │  v161.1 │ 5 days ago │ MAPSRELEASES-12948 │ (@mr-spock) User position quality │
   └─────────┴────────────┴────────────────────┴───────────────────────────────────┘
   ┌ Release (start) candidates ────────┬───────────────────────────────────────────────────────────────────┐
   │  Version │ Created    │ Sb task    │ Comment                                                           │
   ├──────────┼────────────┼────────────┼───────────────────────────────────────────────────────────────────┤
   │ r8737055 │ 3 days ago │ 1101275489 │ (@euclid) NMAPS-14420 add point geometry to image_overlay/public. │
   └──────────┴────────────┴────────────┴───────────────────────────────────────────────────────────────────┘
   ```
3. Ищем в таблице "Release (start) candidates" свою ревизию. Если её там нет, то:
   1) Ещё раз убеждаемся, что нужные изменения закоммичены.
   2) Проверяем, что в данный момент в тестинг выкачена более ранняя ревизия, а не ваша или более поздняя, которая уже содержит ваши изменения.
   3) Если ничего не понятно, то вызываем [~~экзорциста~~специалиста](#sos)
4. Очень важно: если в списке кандидатов кроме вашей ревизии есть ещё чьи-то и они тоже выкатятся, нужно быть абсолютно уверенным, что их можно выкатывать. Если уверенности нет, то нужно спросить у автора коммита, либо задуматься о создании хотфикса.
5. Запускаем выкатку заклинанием `sedem release start <service-path> <revision>` (попросит подтверждение). Вариант чуть попроще - выкатить самую свежую доступную ревизию, для этого используем ту же команду без указания revision.
[Новый снапшот в няне](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_maintenance_testing/) начинает выкатываться практически сразу.
6. Если катим редактор, нужно катить два сервиса: editor/reader и editor/writer. В этих сервисах **всегда** должна быть одна и та же ревизия.


### Выкладка самых свежих докеров сразу всех сервисов в тестинг (кроме maintenance)

1. Проходим [чеклист](#checklist) самопроверки перед выкатыванием.
2. "Катим" метасервис nmaps командой `sedem release start nmaps`
   ```
   chikunov@maps-nmaps-dev:~/arc/arcadia/maps/wikimap/mapspro/services$ sedem release start nmaps
   Loading service state..........................................................................................................
   maps-core-nmaps-acl:
     Will create and deploy to testing release v127.1 (r8737055): (@euclid) NMAPS-14420 add point geometry to image_overlay/public.
   maps-core-nmaps-dataset-explorer:
     WARNING: No candidates available for release
     (use "sedem release build ..." to make one)
   maps-core-nmaps-editor:
     Will create and deploy to testing release v226.1 (r8743038): (@euclid) Design NMAPSDESIGN-120 +  hot fix.
     WARNING: Possible downgrade: commit r8743038 is older than the one in testing
   maps-core-nmaps-editor-writer:
     Will create and deploy to testing release v226.1 (r8743038): (@euclid) Design NMAPSDESIGN-120 +  hot fix.
     WARNING: Possible downgrade: commit r8743038 is older than the one in testing
   maps-core-nmaps-gdpr:
     WARNING: No candidates available for release
     (use "sedem release build ..." to make one)
   maps-core-nmaps-grinder:
     WARNING: No candidates available for release
     (use "sedem release build ..." to make one)
   maps-core-nmaps-renderer-nmaps:
     Will create and deploy to testing release v98.1 (r8743038): (@euclid) Design NMAPSDESIGN-120 +  hot fix.
     WARNING: Possible downgrade: commit r8743038 is older than the one in testing
   maps-core-nmaps-renderer-overlay:
     WARNING: No candidates available for release
     (use "sedem release build ..." to make one)
   maps-core-nmaps-social:
     Will create and deploy to testing release v190.1 (r8739442): (@vbystricky) Добавил аттрибуты в гипотезу запрета манёвра
   maps-core-nmaps-social-backoffice:
     Will create and deploy to testing release v59.1 (r8739442): (@vbystricky) Добавил аттрибуты в гипотезу запрета манёвра
   maps-core-nmaps-tasks:
     WARNING: No candidates available for release
     (use "sedem release build ..." to make one)
   maps-core-nmaps-tasks-export:
     Will create and deploy to testing release v164.1 (r8738375): (@euclid) NMAPS-14420 make complete point addition to image overlay.
   maps-core-nmaps-tasks-feedback:
     Will create and deploy to testing release v145.1 (r8739442): (@vbystricky) Добавил аттрибуты в гипотезу запрета манёвра
   maps-core-nmaps-tasks-misc:
     Will create and deploy to testing release v129.1 (r8743038): (@euclid) Design NMAPSDESIGN-120 +  hot fix.
   maps-core-nmaps-tasks-realtime:
     Will create and deploy to testing release v162.1 (r8743038): (@euclid) Design NMAPSDESIGN-120 +  hot fix.
   maps-core-nmaps-tasks-social:
     Will create and deploy to testing release v108.1 (r8739442): (@vbystricky) Добавил аттрибуты в гипотезу запрета манёвра
   maps-core-nmaps-tasks-sprav:
     Will create and deploy to testing release v157.1 (r8738375): (@euclid) NMAPS-14420 make complete point addition to image overlay.
   maps-core-nmaps-tasks-yt:
     Will create and deploy to testing release v150.1 (r8738375): (@euclid) NMAPS-14420 make complete point addition to image overlay.
   Proceed to creation and deployment? [y/N]: 
   ```
   Типичные варнинги
   1. `Possible downgrade: commit r8743038 is older than the one in testing` - скорее всего, кто-то выкатывал хотфикс в тестинг. Можно проигнорировать.
   2. `No candidates available for release` - self explanatory. Можно игнорировать.
3. Мониторим состояние выкатки через [пресет в infra](https://infra.yandex-team.ru/timeline?preset=KTtDs8gmSVG).


## Накатывание миграций и wiki-acl-tool

Для миграций и wiki-acl-tool заведён отдельный сервис maps-core-nmaps-maintenance, который катится отдельно от остальных, чтобы иметь возможность произвести манипуляции с БД до выкатки софта. Перед тем, как что либо делать, нужно убедиться, что новая версия соответствующего стейджинга сервиса maps-core-nmaps-maintenance выкачена. Для этого заходим в Nanny-сервис maps_core_nmaps_maintenance_$staging и осуществляем визуальный контроль выкатки нового снапшота. Когда снапшот перейдёт в состояние Active, можно зайти в Container access (кнопка с облачком слева) любого (единственного) инстанса и скопировать команду для SSH (вторая строка, длинная команда с полным указанием конфигурации). Да, portoshell тоже подойдёт.

Доступные стейджинги: unstable, testing, stable.

### Миграции <a name="migrations"></a>

##### TL;DR:

1. Проверить, есть ли новые миграции: `maintenance> nmaps-pgmigrate check`
1. Накатить миграции: `maintenance> nmaps-pgmigrate upgrade`

**Миграции накатываются по отдельности в каждом стейджинге ([unstable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_maintenance_unstable/),[testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_maintenance_testing/),[stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_maintenance_stable/)).**

`NONTRANSACTIONAL` миграции нужно накатывать отдельно. Для этого используйте команду вида `nmaps-pgmigrate upgrade -t 529`.

Если миграция фейлится и непонятно, что делать, нужно идти в maps-wiki-dev за помощью.
Если миграция вида `CREATE INDEX CONCURRENTLY` фейлится с `canceling statement due to lock timeout`, то можно попробовать добавить перед созданием индекса прямо в миграцию `set lock_timeout=0;`, почистить недосозданный индекс и накатить миграцию ещё раз. (У нас на отдельных базах стоит ненулевой lock_timeout. Способ работает только с pooling_mode=session)

### Права, они же пермишоны <a name="permissions"></a>

Обновления прав, описанные в permissions.xml, заносятся в базу с помощью wiki-acl-tool:
   ```
   maintenance> /usr/lib/yandex/maps/wiki/bin/wiki-acl-tool --default
   ```
Режим `--default` использует подключение к базе, описанное в конфиге `/etc/yandex/maps/wiki/services/services.xml`, и файл с правами, находящийся в `/usr/share/yandex/maps/wiki/editor/permissions.xml`. При необходимости можно переопределить эти пути с помощью опций `--config` и `--permissions` соответственно.

При обновлении прав с удалением старых может показаться сообщение такого рода:
```
path mpro/social/feedback/task/startrek-link
      Assigned to roles: 
        need_info
        feedback_read
        feedback_other
        basic-cartographer-tools
        feedback_manager
        cartographer
(S)kip and continue adding, (D)elete from database then add, (C)ancel operation:
```
Это означает, что какое-то право удалено из нового дерева, но в базе есть роли ссылающиеся на него.
Обычно можно нажать D (удалить и продолжить), но если есть сомнения, можно предупредить отвественных за права, что у ролей меняется набор прав.

## Ручное подтверждение в nanny <a name="ruchnoepodtverzhdenievnanny"></a>

Есть сервисы, которые выполняют долгие операции.
Если эти операции прервать, то, например, придётся заново выполнять 8-мичасовую операцию, и есть шанс получить не консистентные данные в базе.

Это сервисы: [tasks_misc](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_tasks_misc_stable/) и [tasks_export](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_tasks_export_stable/).
Выкатка этих сервисов в **stable** требует ручного подтверждения в nanny.


### Как вручную подтвердить выкатку

1. Открыть нужный сервис в nanny.
2. Нажать на ссылку **Taskgroup** ожидающего подтверждения снапшота.
3. Выбрать **Task** с пометкой **NEEDS_CONFIRM**.
4. Нажать кнопку **Confirm**.


### Когда можно подтверждать выкатку [tasks_misc](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_tasks_misc_stable/) <a name="tasksmiscconfirm"></a>

Открыть [nmaps](https://n.maps.yandex.ru/#!/tools/longtasks?type=groupedit&z=20&ll=36.964191%2C55.808133&l=nk%23sat).
Проверить, что нет запущенных задач с типами: импорт, подготовка релизной ветки, синхронизация представлений, групповое редактирование.

Если есть, подождать.
Можно спросить автора задачи, когда ожидается завершение задачи.


### Когда можно подтверждать выкатку [tasks_export](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_tasks_export_stable/) <a name="tasksexportconfirm"></a>

Открыть [nmaps](https://n.maps.yandex.ru/#!/tools/longtasks?type=export&z=20&ll=36.964191%2C55.808133&l=nk%23sat).
Проверить, что нет запущенных задач с типами: экспорт, пакетный запуск валидации и экспорта.

Если есть, подождать.
Можно спросить автора задачи, когда ожидается завершение задачи.


## Хотфиксы

Хотфиксы выполняются посервисно согласно [штатной инструкции к sedem release](https://docs.yandex-team.ru/sedem/releases). Для каждого затронутого сервиса выполняются две команды: `sedem release hotfix` для создания образа и `sedem release step` для выкатки в нужный стейджинг.
