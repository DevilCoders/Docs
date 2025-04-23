## nightly baseline
**сервисы няни**

* [search controller](https://nanny.yandex-team.ru/ui/#/services/catalog/man_nightlybaseline_search_controller/)
    - [basesearch](https://nanny.yandex-team.ru/ui/#/services/catalog/nightlybaseline_jupiter_base/)
    - [deployer](https://nanny.yandex-team.ru/ui/#/services/catalog/nightlybaseline_jupiter_deploy/)
    - [builder](https://nanny.yandex-team.ru/ui/#/services/catalog/nightlybaseline_jupiter_build/)

**не управляются контроллерами**

- [int](https://nanny.yandex-team.ru/ui/#/services/catalog/nightlybaseline_jupiter_int/)
- [mmeta](https://nanny.yandex-team.ru/ui/#/services/catalog/nightlybaseline_jupiter_mmeta/)

**ресурсы генерилки**

- PlatinumTier0, пачка групп и интлукапов

**поисковая бета**

- [sdms balancer](https://sdms.yandex-team.ru/balancer/key/.*nightlybaseline%5C.hamster%5C.yandex%5C.%28ru%7Cua%7Ckz%7Cby%7Ccom%7Ccom.tr%29)
- [nightlybaseline.hamster.yandex.ru](https://nightlybaseline.hamster.yandex.ru/)

## nightly test
**сервисы няни**

* [search controller](https://nanny.yandex-team.ru/ui/#/services/catalog/man_nightlytest_search_controller/)
    - [basesearch](https://nanny.yandex-team.ru/ui/#/services/catalog/nightlytest_jupiter_base/)
    - [deployer](https://nanny.yandex-team.ru/ui/#/services/catalog/nightlytest_jupiter_deploy/)
    - [builder](https://nanny.yandex-team.ru/ui/#/services/catalog/nightlytest_jupiter_build/)

**не управляются контроллерами**

- [int](https://nanny.yandex-team.ru/ui/#/services/catalog/nightlytest_jupiter_int/)
- [mmeta](https://nanny.yandex-team.ru/ui/#/services/catalog/nightlytest_jupiter_mmeta/)

**ресурсы генерилки**

- PlatinumTier0, пачка групп и интлукапов

**поисковая бета**

- [sdms balancer](https://sdms.yandex-team.ru/balancer/key/.*nightlytest%5C.hamster%5C.yandex%5C.%28ru%7Cua%7Ckz%7Cby%7Ccom%7Ccom.tr%29)
- [nightlytest.hamster.yandex.ru](https://nightlytest.hamster.yandex.ru/)
===

**схема работы автоматики**
1) допустим ты хочешь выкатить стейт 2017-01-23 12:34:45 на baseline
2) идешь в yt и прописываешь 20170123-123445 в //home/jupiter-test/index_deploy/nightly_baseline в атрибут deploy_params/state - после этого начинает работать автоматика по выгрузке на нашей стороне
3) можно смотреть в http://nightlybaseline-search.n.yandex-team.ru/viewer
4) периодически дергаешь http://nightlybaseline-search.n.yandex-team.ru/status , как только в state/observed/timestamp появляется 1485174885 (это unix timestamp от 20170123-123445) - бета готова
