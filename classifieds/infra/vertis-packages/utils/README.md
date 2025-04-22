# Utils

Папка для всяческих утилит, полезных при сборке пакетов этого репо.


## compile\_nginx\_configs.sh

Запускается обязательно из папки _utils_.
Создает папку _tmp_ и собирает в нее конфиги nginx для последующего тестирования.
Берутся конфиги из _yandex-vertis-config-nginx-common_ текущего репо и фрагменты из первого аргумента для скрипта.
Пример:
```
 ~/ans/vertis-packages/utils  pwd
/home/user/ans/vertis-packages/utils

 ~/ans/vertis-packages/utils  ./compile_nginx_configs.sh yandex-vertis-config-nginx-front-mini

 ~/ans/vertis-packages/utils  tree tmp/ -L 1
tmp/
├── conf.d
├── include
├── nginx.conf
└── sites-enabled

3 directories, 1 file
```


Можно запустить вручную тестирование при помощи yodax, которое на каждый коммит гоняет Teamcity:
```
 ~/ans/vertis-packages/utils  for cname in autoru-api front-external front-internal front-mini front-realty;do rm -fr tmp/*; \
 echo -e "\n#####\t$cname\t####\n";./compile_nginx_configs.sh yandex-vertis-config-nginx-$cname; \
 docker run -ti --rm=true -v /home/user/ans/vertis-packages/:/mnt/nginx registry.vertis.yandex.net/yodax:latest;echo $?;done

#####   autoru-api      ####

[nginx_parser]  WARNING File not found: /etc/nginx/mime.types

==================== Results ===================
No issues found.

==================== Summary ===================
Total issues:
    Unspecified: 0
    Low: 0
    Medium: 0
    High: 0

0

#####   front-external  ####

[nginx_parser]  WARNING File not found: /etc/nginx/mime.types
[nginx_parser]  WARNING File not found: /etc/nginx/include/allowyandexnets.inc
[nginx_parser]  WARNING File not found: /etc/nginx/include/allowyandexnets.inc
[nginx_parser]  WARNING File not found: /etc/nginx/include/allowyandexnets.inc

==================== Results ===================
No issues found.

==================== Summary ===================
Total issues:
    Unspecified: 0
    Low: 0
    Medium: 0
    High: 0

0

#####   front-internal  ####

[nginx_parser]  WARNING File not found: /etc/nginx/mime.types
[nginx_parser]  WARNING File not found: /etc/nginx/include/allowyandexnets.inc
[nginx_parser]  WARNING File not found: /etc/nginx/include/allowyandexnets.inc
[nginx_parser]  WARNING File not found: /etc/nginx/include/allowyandexnets.inc

==================== Results ===================
No issues found.

==================== Summary ===================
Total issues:
    Unspecified: 0
    Low: 0
    Medium: 0
    High: 0

0

#####   front-mini      ####

[nginx_parser]  WARNING File not found: /etc/nginx/mime.types
[nginx_parser]  WARNING File not found: /etc/nginx/include/management-api.vertis.yandex.net/upstream-notmatch-backend-management-api.inc
[nginx_parser]  WARNING File not found: /etc/nginx/include/nomad.vertis.yandex.net/upstream-notmatch-backend-nomad.inc
[nginx_parser]  WARNING File not found: /etc/nginx/include/hooker.vertis.yandex.net/upstream-notmatch-backend-hooker.inc
[nginx_parser]  WARNING File not found: /etc/nginx/include/st-api.vertis.yandex.net/upstream-notmatch-backend-st-api.inc
[nginx_parser]  WARNING File not found: /etc/nginx/include/realty-admin.vertis.yandex-team.ru/upstream-notmatch-backend-realty-admin.inc
[nginx_parser]  WARNING File not found: /etc/nginx/include/hobo.vertis.yandex-team.ru/upstream-notmatch-backend-hobo.inc
[nginx_parser]  WARNING File not found: /etc/nginx/include/user-clustering.vertis.yandex.net/upstream-notmatch-backend-user-clustering.inc
[nginx_parser]  WARNING File not found: /etc/nginx/include/moderation.vertis.yandex.net/upstream-notmatch-backend-nodejs-moderation.inc
[nginx_parser]  WARNING File not found: /etc/nginx/include/zipkin.vertis.yandex.net/upstream-notmatch-backend-zipkin.inc
[nginx_parser]  WARNING File not found: /etc/nginx/include/zookeeper.vertis.yandex.net/upstream-notmatch-backend-zookeeper.inc
[nginx_parser]  WARNING File not found: /etc/nginx/include/pilot.vertis.yandex-team.ru/upstream-notmatch-backend-pilot.inc
[nginx_parser]  WARNING File not found: /etc/nginx/include/parts-admin.vertis.yandex.net/upstream-notmatch-backend-parts-admin.inc
[nginx_parser]  WARNING File not found: /etc/nginx/include/superset.vertis.yandex.net/upstream-notmatch-backend-superset.inc
[nginx_parser]  WARNING File not found: /etc/nginx/include/broccoli.vertis.yandex.net/upstream-notmatch-backend-broccoli.inc
[nginx_parser]  WARNING File not found: /etc/nginx/include/hprof.vertis.yandex.net/upstream-notmatch-backend-hprof.inc

==================== Results ===================
No issues found.

==================== Summary ===================
Total issues:
    Unspecified: 0
    Low: 0
    Medium: 0
    High: 0

0

#####   front-realty    ####

[nginx_parser]  WARNING File not found: /etc/nginx/mime.types
[nginx_parser]  WARNING File not found: /etc/nginx/include/realty.yandex.ru/upstreams-realty.yandex.ru.inc
[context]       INFO    Can't find variable 'upstream_dc_realty'
[context]       INFO    Can't find variable 'upstream_dc_realty'
[context]       INFO    Can't find variable 'upstream_dc_realty'
[context]       INFO    Can't find variable 'upstream_dc_realty'

==================== Results ===================
No issues found.

==================== Summary ===================
Total issues:
    Unspecified: 0
    Low: 0
    Medium: 0
    High: 0

0
```
