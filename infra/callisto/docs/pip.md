PIP stands for Priemka in Production

Запускается над подмножеством базы: PlatinumTier0, WebTier1/local,
WebTier1/remote\_storage, MsuseardataJupiterTier0,
EmbeddingWebTier1, InvertedIndexWebTier1

**сервисы няни**
* [search controller](https://nanny.yandex-team.ru/ui/#/services/catalog/web-prod-acceptance-controller/)
    - [deployer](https://nanny.yandex-team.ru/ui/#/services/catalog/cajuper_deploy_pip/)
    - [basesearch PlatinumTier0](https://nanny.yandex-team.ru/ui/#/services/catalog/cajuper_web_platinum_base_pip/)
    - [basesearch WebTier1/local](https://nanny.yandex-team.ru/ui/#/services/catalog/cajuper_web_tier1_base_pip/)
    - [EmbeddingWebTier1](https://nanny.yandex-team.ru/ui/#/services/catalog/vla_jupiter_embedding_pip/)
    - [InvertedIndexWebTier1](https://nanny.yandex-team.ru/ui/#/services/catalog/vla_jupiter_inverted_index_pip/)
    - [mmeta](https://nanny.yandex-team.ru/ui/#/services/catalog/cajuper_mmeta_pip/)

сервис remote storage pip получает конфиги из [sb task](https://sandbox.yandex-team.ru/tasks/?type=SWITCH_PIP_CONFIGS)
и по сути управляется не контроллером, а таском
    - [remote\_storage WebTier1](https://nanny.yandex-team.ru/ui/#/services/catalog/vla_jupiter_remote_storage_pip/)


**не управляются контроллерами**
- [int L2](https://nanny.yandex-team.ru/ui/#/services/catalog/jupiter_int_pip/)
- [int](https://nanny.yandex-team.ru/ui/#/services/catalog/jupiter_int_l1_pip/)

**ресурсы генерилки**

- VLA\_WEB\_BASE\_PIP\_DEPLOY
- VLA\_WEB\_MMETA\_PIP
- VLA\_WEB\_PLATINUM\_JUPITER\_BASE\_PIP
- VLA\_WEB\_PLATINUM\_JUPITER\_INT\_PIP
- VLA\_WEB\_TIER1\_EMBEDDING\_PIP
- VLA\_WEB\_TIER1\_INVERTED\_INDEX\_PIP
- VLA\_WEB\_TIER1\_JUPITER\_BASE\_PIP
- VLA\_WEB\_TIER1\_JUPITER\_INTL2\_PIP
- VLA\_WEB\_TIER1\_JUPITER\_INT\_PIP
- VLA\_WEB\_TIER1\_REMOTE\_STORAGE\_BASE\_PIP

описание тиров, интлукапы

**поисковая бета**
- [yappy beta](https://yappy.z.yandex-team.ru/b/woogiejpip)
- [woogiejpip.hamster.yandex.ru](https://woogiejpip.hamster.yandex.ru/)

**контрольная бета**
представляет из себя отдельные средние (группа VLA\_WEB\_MMETA\_JPROD), сливающие трафик в прод

- [yappy control beta](https://yappy.z.yandex-team.ru/b/woogiejprod)
- [woogiejprod.hamster.yandex.ru](https://woogiejprod.hamster.yandex.ru)
