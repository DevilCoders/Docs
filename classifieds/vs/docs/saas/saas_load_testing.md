### Нагрузочное тестирование SaaS

Для нагрузочного тестирования используется [Яндекс.Танк](https://yandex.ru/dev/tank/).  
Создать стрельбы можно через https://lunapark.yandex-team.ru/firestarter/.  
Пример валидной конфигурации:
```yaml
phantom:
    address: 'saas-yp-searchproxy-stable-5.man.yp-c.yandex.net:80'
    ammofile: 'https://storage-int.mds.yandex.net/get-load-ammo/21533/c7844ebc04a04e66bfbff1c75acc8d91'
    load_profile: {load_type: rps, schedule: 'const(10,2m)'}
    uris: []
uploader:
    enabled: true
    job_dsc: ""
    job_name: ""
    operator: makarchuk-aa
    package: yandextank.plugins.DataUploader
    meta:
        use_tank: 'nanny:production_yandex_tank'
        use_tank_port: 30169
    task: VS-436
    ver: ""
```

#### Подробнее:
##### address
1. Указывается имя прокси, а не балансера.  
Выбирать прокси нужно из этого списка  
https://saas-mon.n.yandex-team.ru/deploy?service=searchproxy&ctype=stable  
но с 80-м портом.

2. Должен существовать доступ с танка до прокси, примеры заявок на доступ:  
https://puncher.yandex-team.ru/tasks?id=5fa54c99b7aaa77a70723e94  
https://puncher.yandex-team.ru/tasks?id=5fb4eac3b7aaa77a707243de
##### ammofile
Путь до любого файла с патронами который может быть скачен танком.  
Проще всего залить свой файл через веб-форму `firestarter`, получить новую ссылку и вставить в конфиг.  
Патроны создаются в URI-формате (см. https://yandextank.readthedocs.io/en/latest/tutorial.html#uri-style-uris-in-file).  
Пример содержимого файла с патронами:
```
[X-Ya-Service-Ticket: TVM_TICKET]
/?service=vasgen_search_lb&kps=1&timeout=5000000&relev=attr_limit%3D100000000&ms=proto&hr=json&p=0&numdoc=72&pron=pruncount1000&text=велосипед%20<<%20i_epoch:%3E%3D"6"%20<<%20(s_offer_region_g:"213")"
/?service=vasgen_search_lb&kps=1&timeout=5000000&relev=attr_limit%3D100000000&ms=proto&hr=json&p=0&numdoc=72&pron=pruncount1000&text=холодильник%20<<%20i_epoch:%3E%3D"6"%20<<%20(s_offer_region_g:"213")"
```
`TVM_TICKET` для `SAAS STABLE` можно получить запустив `vasgen-searcher` локально с конфигурацией `SearcherApp_PROD_SAAS.run.xml`.  
Альтернативно можно отключить `TVM` или сделать мок, как написано [здесь](https://wiki.yandex-team.ru/Load/tvm/).  

##### Стрельба по нескольким мишеням

Дока: https://yandextank.readthedocs.io/en/latest/core_and_modules.html#multi-tests

Пример валидной конфигурации:
```yaml
bfg:
    package: yandextank.plugins.Bfg
console:
    enabled: false
phantom:
    address: saas-yp-searchproxy-stable-1.sas.yp-c.yandex.net
    ammofile: 'https://storage-int.mds.yandex.net/get-load-ammo/21533/17f924b8b93b40a48f0ea1201b6f06c2'
    cache_dir: /place/db/www/logs/yandex-tank/tankapi/tests/stpd-cache
    load_profile: {load_type: rps, schedule: 'line(1,300,600s)'}
    multi: [
      {
        address: saas-yp-searchproxy-stable-2.sas.yp-c.yandex.net,
        ammofile: 'https://storage-int.mds.yandex.net/get-load-ammo/21533/17f924b8b93b40a48f0ea1201b6f06c2',
        cache_dir: /place/db/www/logs/yandex-tank/tankapi/tests/stpd-cache,
        load_profile: {load_type: rps, schedule: 'line(1,300,600s)'},
        uris: []
      },
      {
        address: saas-yp-searchproxy-stable-3.sas.yp-c.yandex.net,
        ammofile: 'https://storage-int.mds.yandex.net/get-load-ammo/21533/17f924b8b93b40a48f0ea1201b6f06c2',
        cache_dir: /place/db/www/logs/yandex-tank/tankapi/tests/stpd-cache,
        load_profile: {load_type: rps, schedule: 'line(1,300,600s)'},
        uris: []
      },
      {
        address: saas-yp-searchproxy-stable-4.sas.yp-c.yandex.net,
        ammofile: 'https://storage-int.mds.yandex.net/get-load-ammo/21533/17f924b8b93b40a48f0ea1201b6f06c2',
        cache_dir: /place/db/www/logs/yandex-tank/tankapi/tests/stpd-cache,
        load_profile: {load_type: rps, schedule: 'line(1,300,600s)'},
        uris: []
      },
      {
        address: saas-yp-searchproxy-stable-5.sas.yp-c.yandex.net,
        ammofile: 'https://storage-int.mds.yandex.net/get-load-ammo/21533/17f924b8b93b40a48f0ea1201b6f06c2',
        cache_dir: /place/db/www/logs/yandex-tank/tankapi/tests/stpd-cache,
        load_profile: {load_type: rps, schedule: 'line(1,300,600s)'},
        uris: []
      },
      {
        address: saas-yp-searchproxy-stable-1.vla.yp-c.yandex.net,
        ammofile: 'https://storage-int.mds.yandex.net/get-load-ammo/21533/17f924b8b93b40a48f0ea1201b6f06c2',
        cache_dir: /place/db/www/logs/yandex-tank/tankapi/tests/stpd-cache,
        load_profile: {load_type: rps, schedule: 'line(1,300,600s)'},
        uris: []
      },
      {
        address: saas-yp-searchproxy-stable-2.vla.yp-c.yandex.net,
        ammofile: 'https://storage-int.mds.yandex.net/get-load-ammo/21533/17f924b8b93b40a48f0ea1201b6f06c2',
        cache_dir: /place/db/www/logs/yandex-tank/tankapi/tests/stpd-cache,
        load_profile: {load_type: rps, schedule: 'line(1,300,600s)'},
        uris: []
      },
      {
        address: saas-yp-searchproxy-stable-3.vla.yp-c.yandex.net,
        ammofile: 'https://storage-int.mds.yandex.net/get-load-ammo/21533/17f924b8b93b40a48f0ea1201b6f06c2',
        cache_dir: /place/db/www/logs/yandex-tank/tankapi/tests/stpd-cache,
        load_profile: {load_type: rps, schedule: 'line(1,300,600s)'},
        uris: []
      },
      {
        address: saas-yp-searchproxy-stable-4.vla.yp-c.yandex.net,
        ammofile: 'https://storage-int.mds.yandex.net/get-load-ammo/21533/17f924b8b93b40a48f0ea1201b6f06c2',
        cache_dir: /place/db/www/logs/yandex-tank/tankapi/tests/stpd-cache,
        load_profile: {load_type: rps, schedule: 'line(1,300,600s)'},
        uris: []
      },
      {
        address: saas-yp-searchproxy-stable-5.vla.yp-c.yandex.net,
        ammofile: 'https://storage-int.mds.yandex.net/get-load-ammo/21533/17f924b8b93b40a48f0ea1201b6f06c2',
        cache_dir: /place/db/www/logs/yandex-tank/tankapi/tests/stpd-cache,
        load_profile: {load_type: rps, schedule: 'line(1,300,600s)'},
        uris: []
      }
    ]
    package: yandextank.plugins.Phantom
    uris: []
telegraf:
    package: yandextank.plugins.Telegraf
uploader:
    enabled: true
    meta: {use_tank: 'nanny:production_yandex_tank', use_tank_port: 30169}
    operator: makarchuk-aa
    package: yandextank.plugins.DataUploader
    task: VS-436
```

План нагрузки должен быть одинаковым, иначе будет сложно интерпретировать результаты стрельб.  
В результатах стрельб `RPS` показывается суммарный, а тайминги - усредненные по мишеням.

#### Примеры стрельб:
https://st.yandex-team.ru/VS-436

#### Полезные ссылки:
Дока https://wiki.yandex-team.ru/load/  
Гайды https://wiki.yandex-team.ru/load/guides/  
Как подготовить ammofile https://wiki.yandex-team.ru/load/guides/ammo/  
Про TVM  https://wiki.yandex-team.ru/Load/tvm/  
Доступы и дырки https://wiki.yandex-team.ru/Load/howto/idm-puncher/  
Почему нельзя стрелять в балансер https://neverov.at.yandex-team.ru/986  
Как можно пострелять в (вертикальный) балансер https://wiki.yandex-team.ru/vertis-admin/deploy/load-testing-lunapark/  
Firestarter https://wiki.yandex-team.ru/load/lunapark/firestarter/  
FAQ https://wiki.yandex-team.ru/load/howto/common_errors/  
Yandex-Tank & Lunapark Support: https://t.me/joinchat/BkIYdz-zGT40Ql-TxPZ04A
