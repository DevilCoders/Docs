# Мониторинги

## Database

* **production-main**: https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=cf93d9c8-2f19-4fdc-a986-87c75712e029;dbname=extmaps-carsharing-production
* **production-chat**: https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbn1lro8vp0a216ccqg;dbname=carsharing-support-production
* **production-aux**: https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=00227ece-9b83-4eb0-bf1c-f9c885bba9d6;dbname=prod_drive_db
* **prestable-aux**: https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=e9f713c5-9fa7-401b-9852-bd60b2b83bdd;dbname=prestable_drive_db
* **testing-main**: https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=e4b922c1-9356-43e4-a0fa-6f3d7b54c962;dbname=extmaps-carsharing-testing
* **testing-aux**: https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=3bf6d7b6-3880-4be6-a589-e647a22c9fce;dbname=test_drivesmall_db
* **testing-qa**: https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdb3l5muuv1js70or02b;dbname=extmaps-carsharing-testing-qa
* **testing-st**: https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdb9g5o0a6ifs1l0iib6;dbname=extmaps-carsharing-testing-qa

## Backend
### Приложение Yandex.Drive
* **stable**: https://yasm.yandex-team.ru/template/panel/DriveFrontendHandles/
* **prestable**: https://yasm.yandex-team.ru/template/panel/DriveFrontendHandles/ctype=hamster
* **testing**: https://yasm.yandex-team.ru/template/panel/DriveFrontendHandles/ctype=testing;prj=drive-backend

### Внешние потребители
* **stable**: https://yasm.yandex-team.ru/template/panel/DriveFrontendExternalHandles/
* **prestable**: https://yasm.yandex-team.ru/template/panel/DriveFrontendExternalHandles/ctype=hamster
* **testing**: https://yasm.yandex-team.ru/template/panel/DriveFrontendExternalHandles/ctype=testing;prj=drive-backend

### Сервисное приложение
* **stable**: https://yasm.yandex-team.ru/template/panel/DriveBackendServiceApp/
* **prestable**: https://yasm.yandex-team.ru/template/panel/DriveBackendServiceApp/ctype=hamster;prj=drive-frontend
* **testing**: https://yasm.yandex-team.ru/template/panel/DriveBackendServiceApp/ctype=testing;prj=drive-backend

### Админка
* **stable**: https://yasm.yandex-team.ru/template/panel/DriveFrontendAdminHandles
* **prestable**: https://yasm.yandex-team.ru/template/panel/DriveFrontendAdminHandles/prj=drive-frontend;ctype=hamster
* **testing**: https://yasm.yandex-team.ru/template/panel/DriveFrontendAdminHandles/prj=drive-backend;ctype=testing

### Процессы
* **all**: https://yasm.yandex-team.ru/panel/drive_processes
* **external**: https://yasm.yandex-team.ru/template/panel/external-drive-api/

### Внешние API
* **stable**: https://yasm.yandex-team.ru/template/panel/DriveExternalApi/
* **prestable**: https://yasm.yandex-team.ru/template/panel/DriveExternalApi/ctype=hamster/
* **testing**: https://yasm.yandex-team.ru/template/panel/DriveExternalApi/ctype=testing;prj=drive-backend/

### Freshness
* **stable**: https://yasm.yandex-team.ru/template/panel/DriveFreshness/
* **prestable**: https://yasm.yandex-team.ru/template/panel/DriveFreshness/ctype=hamster/
* **testing**: https://yasm.yandex-team.ru/template/panel/DriveFreshness/ctype=testing;prj=drive-backend/

### Handlers in progress
* **production**: https://yasm.yandex-team.ru/template/panel/DriveHandlersInProgress/
* **leasing**: https://yasm.yandex-team.ru/template/panel/DriveHandlersInProgress/prj=drive-backend-leasing/
* **admin**: https://yasm.yandex-team.ru/template/panel/DriveHandlersInProgress/prj=drive-frontend-admin/
* **chat**: https://yasm.yandex-team.ru/template/panel/DriveHandlersInProgress/prj=drive-backend-chat/
* **service**: https://yasm.yandex-team.ru/template/panel/DriveHandlersInProgress/prj=drive-frontend-service/
* **prestable**: https://yasm.yandex-team.ru/template/panel/DriveHandlersInProgress/ctype=hamster/
* **testing**: https://yasm.yandex-team.ru/template/panel/DriveHandlersInProgress/ctype=testing;prj=drive-backend/


## Balancer
* **stable**: https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=carsharing.yandex.net;itype=balancer;ctype=prestable,prod;metaprj=balancer;locations=man,sas,vla;prj=carsharing;signal=stable_frontend
* **prestable**: https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=carsharing.yandex.net;itype=balancer;ctype=prestable,prod;metaprj=balancer;locations=man,sas,vla;prj=carsharing;signal=prestable_frontend
* **chats**: https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=carsharing.yandex.net;itype=balancer;ctype=prestable,prod;metaprj=balancer;locations=man,sas,vla;prj=carsharing;signal=support_frontend

## Billing
* **stable**: https://yasm.yandex-team.ru/template/panel/DriveBillingNew/
* **prestable**: https://yasm.yandex-team.ru/template/panel/DriveBillingNew/ctype=hamster;prj=drive-frontend/
* **testing**: https://yasm.yandex-team.ru/template/panel/DriveBillingNew/ctype=testing;prj=drive-backend/

{% cut "Old" %}
* **stable**: https://yasm.yandex-team.ru/template/panel/DriveBilling/service=-drive_frontend_robot
* **prestable**: https://yasm.yandex-team.ru/template/panel/DriveBilling/service=-drive_frontend;ctype=prestable_maps/

{% endcut %}

## Trust
* **stable**: https://yasm.yandex-team.ru/template/panel/DriveTrust/
* **prestable**: https://yasm.yandex-team.ru/template/panel/DriveTrust/prj=drive-frontend;ctype=hamster/
* **testing**: https://yasm.yandex-team.ru/template/panel/DriveTrust/prj=drive-backend;ctype=testing/

{% cut "Old" %}
* **stable**: https://yasm.yandex-team.ru/template/panel/DriveBilling3/service=-drive_frontend_robot

{% endcut %}

## Chats
* client: 
  * **stable**: https://yasm.yandex-team.ru/template/panel/DriveChatClientHandles/
  * **prestable**: https://yasm.yandex-team.ru/template/panel/DriveChatClientHandles/ctype=hamster;prj=drive-frontend;service=drive_frontend/
  * **testing**: https://yasm.yandex-team.ru/template/panel/DriveChatClientHandles/ctype=testing;prj=drive-backend;service=drive_frontend_testing/
* admin: 
  * **stable**: https://yasm.yandex-team.ru/template/panel/DriveChatAdminHandles/
  * **prestable**: https://yasm.yandex-team.ru/template/panel/DriveChatAdminHandles/ctype=hamster;prj=drive-frontend;service=drive_frontend/
  * **testing**: https://yasm.yandex-team.ru/template/panel/DriveChatAdminHandles/ctype=testing;prj=drive-backend;service=drive_frontend_testing/
* registration:
  * **stable**: https://yasm.yandex-team.ru/template/panel/DriveChatRegistrationHandles/
  * **prestable**: https://yasm.yandex-team.ru/template/panel/DriveChatRegistrationHandles/ctype=hamster;prj=drive-frontend;service=drive_frontend/
  * **testing**: https://yasm.yandex-team.ru/template/panel/DriveChatRegistrationHandles/ctype=testing;prj=drive-backend;service=drive_frontend_testing/

## Health

* **production**: https://yasm.yandex-team.ru/template/panel/DriveServerHealth/
* **admin**: https://yasm.yandex-team.ru/template/panel/DriveServerHealth/prj=drive-frontend-admin/
* **service**: https://yasm.yandex-team.ru/template/panel/DriveServerHealth/prj=drive-frontend-service/
* **robot**: https://yasm.yandex-team.ru/template/panel/DriveServerHealth/prj=drive-backend-robot/
* **chat**: https://yasm.yandex-team.ru/template/panel/DriveServerHealth/prj=drive-backend-chat/
* **prestable**: https://yasm.yandex-team.ru/template/panel/DriveServerHealth/prj=drive-frontend;ctype=hamster/
* **testing**: https://yasm.yandex-team.ru/template/panel/DriveServerHealth/prj=drive-backend;ctype=testing/
* **qa**: https://yasm.yandex-team.ru/template/panel/DriveServerHealth/prj=drive-frontend-qa;ctype=testing/
* **st**: https://yasm.yandex-team.ru/template/panel/DriveServerHealth/prj=drive-frontend-st;ctype=testing/

## Misc
* **handlers in progress**: https://yasm.yandex-team.ru/template/panel/handlers-in-progress/
* **DriveChatCluster**: https://yasm.yandex-team.ru/panel/DriveChatCluster

## Telematics
### Connections
* **stable**: https://yasm.yandex-team.ru/template/panel/DriveTelematicsConnections/service=drive_telematics_production/
* **prestable**: https://yasm.yandex-team.ru/template/panel/DriveTelematicsConnections/service=drive_telematics_prestable/
* **testing**: https://yasm.yandex-team.ru/template/panel/DriveTelematicsConnections/service=drive_telematics_testing/

### Health
* **stable**: https://yasm.yandex-team.ru/template/panel/DriveTelematicsServerHealth/service=drive_telematics_production/
* **prestable**: https://yasm.yandex-team.ru/template/panel/DriveTelematicsServerHealth/service=drive_telematics_prestable/
* **testing**: https://yasm.yandex-team.ru/template/panel/DriveTelematicsServerHealth/service=drive_telematics_testing/

## SaaS
* **drive_features (stable)**: https://saas-mon.n.yandex-team.ru/monitor?ctype=stable_kv&service=drive_features&kind=proxy
* **drive_features (prestable)**: https://saas-mon.n.yandex-team.ru/monitor?ctype=prestable&service=drive_features&kind=proxy&dc=&allserv=

## YDB

* [production](https://yc.yandex-team.ru/folders/fooainf7nqpbcjc1891d/ydb/databases/etn03td697j8h036p56s/monitoring).
* [testing](https://yc.yandex-team.ru/folders/fooainf7nqpbcjc1891d/ydb/databases/etn022p3kh05vhqfafrm/monitoring).

## Misc
**DriveFrontend-histograms** 
https://yasm.yandex-team.ru/template/panel/DriveFrontend-histograms/
