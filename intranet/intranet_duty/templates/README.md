## Графики и основные алерты бекэнда и фронтэнда

```
{{iframe
src="//yasm.yandex-team.ru/template/panel/duty-computer-backend-production/service_name=dogma_intranet;prj=tools.dogma.production;ctype=dogma;dbs_info=[{'cid':'1dee1c9c-d31f-4e3b-904d-90de936261a5','name':'dogma'},{'cid':'1dee1c9c-d31f-4e3b-904d-90de936261a5','name':'dogma'}]?fullscreen=1"
width="100%" height="1450px"}}
```

в `dbs_info` - массив с данными базы в виде `[{'cid': 'cid_базы', 'name': 'name_базы'}]` (можно указать несколько баз)

## Все алёрты сервиса
Удобно выводить на телевизор, чтобы видеть полную картину по сервису. Входным параметром служит слаг ABC сервиса, который вы выбрали для директории с конфигами алертов, например, [для Коннекта](https://yasm.yandex-team.ru/template/panel/common_service_alerts_template/abc=directory/?fullscreen=1) это `directory`.

## Deploy
В `common_backend_template_deploy` поддержаны графики на деплой/авакс/postgres
пример: https://yasm.yandex-team.ru/template/panel/commong_backend_deploy/service_name=abc_back_production;stage=tools-abc-back-production;awacs_prj=tools-abc-testing.stable.tools.yandex-team.ru;deploy_units=['backend-financial-resources','celery'];dbs_info=[%7B'cid':'caeba73b-3501-4751-9d10-ad600dc20cf1','name':'abcdb'%7D]/
