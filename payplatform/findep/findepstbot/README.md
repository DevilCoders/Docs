findepstbot
================

findep bot with startrek hooks

to run 
```bash
ya make && PAYSYS_WSGI_HOST=localhost PAYSYS_ST_OAUTH_TOKEN="AQAD-XXXXXX" ./findepstbot-app
```

to build and upload docker container
```bash
ya package --docker --docker-push --target-platform linux  --docker-repository paysys-test package.json
```

application is hosted here: https://platform.yandex-team.ru/projects/paysys/findepstbot
development url of service: https://findepstbot-dev.paysys.yandex.net/
test (aka prod) https://findepstbot-test.paysys.yandex.net

curl example
```bash
curl -H "content-type: application/json" -XPOST --data '{"issue_key": "DOCSCSDEV-2269", "method": "group_edit", "header_re": "Закрывающие Документы, #ЗП (?P<zp_number>[0-9]+)", "header_tpl": "Закрывающие Документы, #ЗП {zp_number}", "attribute": "email"}' localhost:8080/startrek_hook
```

configure startrek
================

Go to administration/automation/triggers (https://st.yandex-team.ru/admin/queue/DOCSCSDEV/triggers/ for example).
add trigger:
   Method: POST
   Address: https://findepstbot-dev.paysys.yandex.net/startrek_hook
   Body:
```json
{
"issue_key": "{{issue.key}}",
"comment_id": "{{comment.id}}",
"method": "comment2attribute",
"attribute_name": "devComment",
"comment_slice": [null, 20],
"notify": false
}
```