# Staff
* [Testing version](https://deploy.yandex-team.ru/stages/tools_staff_testing)
* [Production version](https://deploy.yandex-team.ru/stages/tools_staff_production)
  
Не забудьте установить python interpreter path: python3

## Релиз с помощью releaser:

* Если releaser не установлен, то установить его
```
ya tool releaser
```
Установка ya tool: https://docs.yandex-team.ru/devtools/intro/quick-start-guide.
Описание releaser: https://a.yandex-team.ru/arc/trunk/arcadia/tools/releaser.
* Скачать проект
```
git clone git@github.yandex-team.ru:tools-sox/staff.git
cd staff
```
* Запустить сборку releaser`ом
```
ya tool releaser release
```
... releaser выставит новую версию, обновит changelog, соберёт docker-образ с новой версией, запушит его в registry и запустит деплой в соответствии с настройками из файла ```.release.hjson```

## Выкатить testing (https://staff.test.yandex-team.ru)
```
ya tool releaser stand -s tools_staff_testing
```
## Выкатить в production
Делать из ветки master
```bash
ya tool releaser release -e tools_staff_production -dd
```

## Работа со стендами
Стенды живут [здесь](https://deploy.yandex-team.ru/projects/staff_back_testing_environment).
### Как создать стенд
Тут в качестве образца используется stage tools_staff_stand_kirill.
Стенды доступны по URL вида https://stand_name.staff-back-stands.yandex-team.ru/.

**Linux:**
```
export NEW_STAND_NAME=cool_stand # <- set stand name
ya tool dctl get stage tools_staff_stand_kirill > $NEW_STAND_NAME.yaml
sed -i "s/kirill.staff/$NEW_STAND_NAME.staff/g" $NEW_STAND_NAME.yaml
ya tool dctl copy stage ./$NEW_STAND_NAME.yaml tools_staff_stand_$NEW_STAND_NAME
rm $NEW_STAND_NAME.yaml
while result=$(ya tool dctl list endpoint 'tools_staff_stand_'$NEW_STAND_NAME'.back' | grep ' True |'); [ "$result" == '' ]; do sleep 5; done
while result=$(ya tool dctl list endpoint 'tools_staff_stand_'$NEW_STAND_NAME'.front' | grep ' True |'); [ "$result" == '' ]; do sleep 5; done
curl -X POST https://awacs.yandex-team.ru/api/CreateBackend/ -d '{"meta":{"id":"'$NEW_STAND_NAME'_front","namespace_id":"staff-back-stands-awacs-balancer.in.yandex-team.ru","comment":"Initial commit","auth":{"type":"STAFF","staff":{"owners":{"logins":[],"group_ids":[]}}}},"spec":{"selector":{"type":"YP_ENDPOINT_SETS_SD","nannySnapshots":[],"gencfgGroups":[],"ypEndpointSets":[{"cluster":"myt","endpointSetId":"tools_staff_stand_'$NEW_STAND_NAME'.front"}],"balancers":[]},"labels":{}},"validateYpEndpointSets":true}' -H "Content-Type: application/json" -H 'Authorization:OAuth '$(<~/.dctl/token)
curl -X POST https://awacs.yandex-team.ru/api/CreateBackend/ -d '{"meta":{"id":"'$NEW_STAND_NAME'_back","namespace_id":"staff-back-stands-awacs-balancer.in.yandex-team.ru","comment":"Initial commit","auth":{"type":"STAFF","staff":{"owners":{"logins":[],"group_ids":[]}}}},"spec":{"selector":{"type":"YP_ENDPOINT_SETS_SD","nannySnapshots":[],"gencfgGroups":[],"ypEndpointSets":[{"cluster":"myt","endpointSetId":"tools_staff_stand_'$NEW_STAND_NAME'.back"}],"balancers":[]},"labels":{}},"validateYpEndpointSets":true}' -H "Content-Type: application/json" -H 'Authorization:OAuth '$(<~/.dctl/token)
curl -X POST https://awacs.yandex-team.ru/api/CreateUpstream/ -d '{"meta":{"id":"'$NEW_STAND_NAME'_front","namespaceId":"staff-back-stands-awacs-balancer.in.yandex-team.ru","comment":"Initial commit","auth":{"type":"STAFF","staff":{"owners":{"logins":[],"group_ids":[]}}}},"spec":{"type":"YANDEX_BALANCER","yandexBalancer":{"mode":"EASY_MODE2","yaml":"l7_upstream_macro:\r\n  version: 0.1.1\r\n  id: '$NEW_STAND_NAME'_front\r\n  compression: {}\r\n  matcher:\r\n    host_re: '$NEW_STAND_NAME'.staff-back-stands.yandex-team.ru\r\n  flat_scheme:\r\n    balancer:\r\n      attempts: 2\r\n      fast_attempts: 2\r\n      max_reattempts_share: 0.15\r\n      max_pessimized_endpoints_share: 0.2\r\n      retry_http_responses:\r\n        codes:\r\n          - 5xx\r\n        exceptions:\r\n          - 500\r\n      backend_timeout: 60s\r\n      connect_timeout: 70ms\r\n    backend_ids:\r\n      - '$NEW_STAND_NAME'_front\r\n    on_error:\r\n      static:\r\n        status: 504\r\n        content: Service unavailable\r\n"},"labels":{"order":"01000000"}}}' -H "Content-Type: application/json" -H 'Authorization:OAuth '$(<~/.dctl/token)
curl -X POST https://awacs.yandex-team.ru/api/CreateUpstream/ -d '{"meta":{"id":"'$NEW_STAND_NAME'_back","namespaceId":"staff-back-stands-awacs-balancer.in.yandex-team.ru","comment":"Initial commit","auth":{"type":"STAFF","staff":{"owners":{"logins":[],"group_ids":[]}}}},"spec":{"type":"YANDEX_BALANCER","yandexBalancer":{"mode":"EASY_MODE2","yaml":"l7_upstream_macro:\r\n  version: 0.1.1\r\n  id: '$NEW_STAND_NAME'_back\r\n  compression: {}\r\n  matcher:\r\n    and_:\r\n      - host_re: '$NEW_STAND_NAME'.staff-back-stands.yandex-team.ru\r\n      - or_:\r\n        - path_re: /api/.*\r\n        - path_re: /admin/.*\r\n        - path_re: /static/.*\r\n        - path_re: /profile-api/.*\r\n        - path_re: /departments-api/.*\r\n        - path_re: /proposal-api/.*\r\n        - path_re: /budget-position-api/.*\r\n        - path_re: /filters-api/.*\r\n        - path_re: /map-api/.*\r\n        - path_re: /card-api/.*\r\n        - path_re: /gap-api/.*\r\n  rewrite:\r\n    - target: PATH\r\n      pattern: {re: ^/api/(.*)$}\r\n      replacement: /%1\r\n  flat_scheme:\r\n    balancer:\r\n      attempts: 2\r\n      fast_attempts: 2\r\n      max_reattempts_share: 0.15\r\n      max_pessimized_endpoints_share: 0.2\r\n      retry_http_responses:\r\n        codes:\r\n          - 5xx\r\n        exceptions:\r\n          - 500\r\n      backend_timeout: 60s\r\n      connect_timeout: 70ms\r\n    backend_ids:\r\n      - '$NEW_STAND_NAME'_back\r\n    on_error:\r\n      static:\r\n        status: 504\r\n        content: Service unavailable\r\n"},"labels":{"order":"00100000"}}}' -H "Content-Type: application/json" -H 'Authorization:OAuth '$(<~/.dctl/token)
echo -e "The stand will be available in few minutes here: \e[0;36mhttps://$NEW_STAND_NAME.staff-back-stands.yandex-team.ru/\e[0m"
```
**macOS:**
```
export NEW_STAND_NAME=cool_stand # <- set stand name
ya tool dctl get stage tools_staff_stand_kirill > $NEW_STAND_NAME.yaml
sed -i '' "s/kirill.staff/$NEW_STAND_NAME.staff/g" $NEW_STAND_NAME.yaml
ya tool dctl copy stage ./$NEW_STAND_NAME.yaml tools_staff_stand_$NEW_STAND_NAME
rm $NEW_STAND_NAME.yaml
while result=$(ya tool dctl list endpoint 'tools_staff_stand_'$NEW_STAND_NAME'.back' | grep ' True |'); [ "$result" == '' ]; do sleep 5; done
while result=$(ya tool dctl list endpoint 'tools_staff_stand_'$NEW_STAND_NAME'.front' | grep ' True |'); [ "$result" == '' ]; do sleep 5; done
curl -X POST https://awacs.yandex-team.ru/api/CreateBackend/ -d '{"meta":{"id":"'$NEW_STAND_NAME'_front","namespace_id":"staff-back-stands-awacs-balancer.in.yandex-team.ru","comment":"Initial commit","auth":{"type":"STAFF","staff":{"owners":{"logins":[],"group_ids":[]}}}},"spec":{"selector":{"type":"YP_ENDPOINT_SETS_SD","nannySnapshots":[],"gencfgGroups":[],"ypEndpointSets":[{"cluster":"myt","endpointSetId":"tools_staff_stand_'$NEW_STAND_NAME'.front"}],"balancers":[]},"labels":{}},"validateYpEndpointSets":true}' -H "Content-Type: application/json" -H 'Authorization:OAuth '$(<~/.dctl/token)
curl -X POST https://awacs.yandex-team.ru/api/CreateBackend/ -d '{"meta":{"id":"'$NEW_STAND_NAME'_back","namespace_id":"staff-back-stands-awacs-balancer.in.yandex-team.ru","comment":"Initial commit","auth":{"type":"STAFF","staff":{"owners":{"logins":[],"group_ids":[]}}}},"spec":{"selector":{"type":"YP_ENDPOINT_SETS_SD","nannySnapshots":[],"gencfgGroups":[],"ypEndpointSets":[{"cluster":"myt","endpointSetId":"tools_staff_stand_'$NEW_STAND_NAME'.back"}],"balancers":[]},"labels":{}},"validateYpEndpointSets":true}' -H "Content-Type: application/json" -H 'Authorization:OAuth '$(<~/.dctl/token)
curl -X POST https://awacs.yandex-team.ru/api/CreateUpstream/ -d '{"meta":{"id":"'$NEW_STAND_NAME'_front","namespaceId":"staff-back-stands-awacs-balancer.in.yandex-team.ru","comment":"Initial commit","auth":{"type":"STAFF","staff":{"owners":{"logins":[],"group_ids":[]}}}},"spec":{"type":"YANDEX_BALANCER","yandexBalancer":{"mode":"EASY_MODE2","yaml":"l7_upstream_macro:\r\n  version: 0.1.1\r\n  id: '$NEW_STAND_NAME'_front\r\n  compression: {}\r\n  matcher:\r\n    host_re: '$NEW_STAND_NAME'.staff-back-stands.yandex-team.ru\r\n  flat_scheme:\r\n    balancer:\r\n      attempts: 2\r\n      fast_attempts: 2\r\n      max_reattempts_share: 0.15\r\n      max_pessimized_endpoints_share: 0.2\r\n      retry_http_responses:\r\n        codes:\r\n          - 5xx\r\n        exceptions:\r\n          - 500\r\n      backend_timeout: 60s\r\n      connect_timeout: 70ms\r\n    backend_ids:\r\n      - '$NEW_STAND_NAME'_front\r\n    on_error:\r\n      static:\r\n        status: 504\r\n        content: Service unavailable\r\n"},"labels":{"order":"01000000"}}}' -H "Content-Type: application/json" -H 'Authorization:OAuth '$(<~/.dctl/token)
curl -X POST https://awacs.yandex-team.ru/api/CreateUpstream/ -d '{"meta":{"id":"'$NEW_STAND_NAME'_back","namespaceId":"staff-back-stands-awacs-balancer.in.yandex-team.ru","comment":"Initial commit","auth":{"type":"STAFF","staff":{"owners":{"logins":[],"group_ids":[]}}}},"spec":{"type":"YANDEX_BALANCER","yandexBalancer":{"mode":"EASY_MODE2","yaml":"l7_upstream_macro:\r\n  version: 0.1.1\r\n  id: '$NEW_STAND_NAME'_back\r\n  compression: {}\r\n  matcher:\r\n    and_:\r\n      - host_re: '$NEW_STAND_NAME'.staff-back-stands.yandex-team.ru\r\n      - or_:\r\n        - path_re: /api/.*\r\n        - path_re: /admin/.*\r\n        - path_re: /static/.*\r\n        - path_re: /profile-api/.*\r\n        - path_re: /departments-api/.*\r\n        - path_re: /proposal-api/.*\r\n        - path_re: /budget-position-api/.*\r\n        - path_re: /filters-api/.*\r\n        - path_re: /map-api/.*\r\n        - path_re: /card-api/.*\r\n        - path_re: /gap-api/.*\r\n  rewrite:\r\n    - target: PATH\r\n      pattern: {re: ^/api/(.*)$}\r\n      replacement: /%1\r\n  flat_scheme:\r\n    balancer:\r\n      attempts: 2\r\n      fast_attempts: 2\r\n      max_reattempts_share: 0.15\r\n      max_pessimized_endpoints_share: 0.2\r\n      retry_http_responses:\r\n        codes:\r\n          - 5xx\r\n        exceptions:\r\n          - 500\r\n      backend_timeout: 60s\r\n      connect_timeout: 70ms\r\n    backend_ids:\r\n      - '$NEW_STAND_NAME'_back\r\n    on_error:\r\n      static:\r\n        status: 504\r\n        content: Service unavailable\r\n"},"labels":{"order":"00100000"}}}' -H "Content-Type: application/json" -H 'Authorization:OAuth '$(<~/.dctl/token)
echo -e "The stand will be available in few minutes here: \e[0;36mhttps://$NEW_STAND_NAME.staff-back-stands.yandex-team.ru/\e[0m"
```

### Выкатить стенд
```
ya tool releaser stand -s stand_name
```

### Балансеры стендов
Балансеры на все стенды общие, живут [тут](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/staff-back-stands-awacs-balancer.in.yandex-team.ru/show/).
Прислоняются через пару [upstream](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/staff-back-stands-awacs-balancer.in.yandex-team.ru/upstreams/list).
Обратите внимание на Labels -> order.
* front [пример](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/staff-back-stands-awacs-balancer.in.yandex-team.ru/upstreams/list/kirill_front/show)
* back [пример](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/staff-back-stands-awacs-balancer.in.yandex-team.ru/upstreams/list/kirill_back/show)

## Сделать миграции
Запускаем bash внутри образа
```bash
docker-compose run backend bash
```
... и там делаем миграции
```bash
staff makemigrations --settings=staff.makemigrations_settings
```

## Запустить тесты
```bash
docker-compose run backend pytest /src/staff
```

## Запустить flake8
```bash
docker-compose run backend python3 -m flake8 /src/staff
```
