# TAXICRM communication campaigns automation service

Very simple Flask application which provides webhooks which are triggered by Forms and Startrek
It exposes POST /api/form/answer which is called by Forms when someone fills in a form [like that](https://forms.yandex-team.ru/admin/30294/edit).

Forms make a callback POST request which provides 2 complex structures: form_info.json and answer_data.json  
Service parses them and converts to a simple flat json.
Then it starts an instance from Hitman project `FORMS_SEGMENTATION` (hardcoded in defaults.conf),
and passes json as a global parameter.

## Deployment
`docker build -t registry.yandex.net/taxi-crm/campaigns-service:latest . && docker push registry.yandex.net/taxi-crm/campaigns-service:latest`

Application is deployed to test environment only (prod is not used).

Then you go to [qloud ui](https://platform.yandex-team.ru/projects/taxi-crm/campaigns-service/test) and update the component.

## Investigations

In case of problems you first check logs of the component, which include both WSGI and application logs.  

If UI logs don't help, then you ssh inside the container and check other logs, modify the code, restart UWSGI service etc.
The most recent form answer is stored in `/var/log/uwsgi`
