## Projects description

Service to store abstract dictionaries

[Design doc](docs/design.md)

[User guide](docs/user_guide.md)

[Api](docs/api.md)


Request queue: https://st.yandex-team.ru/createTicket?type=2&priority=2&queue=VSDATA 

### How to run locally

#### TVM
Palma uses TVM so to run api server locally you will need [TVM_CLIENT_ID and TVM_SECRET]((https://abc.yandex-team.ru/services/VSINFR/resources/?supplier=14&type=47&type=50&state=requested&state=approved&state=granted&view=consuming&show-resource=19098581)) to be set in environment.
Or you can use config with tvm = null to run without TVM.

#### YandexInternalCertificate
Some of internal services, which Palma uses, are closed with YandexInternalRootCa (like Shiva Public Api).
To correct work with that services locally you should [patch](https://wiki.yandex-team.ru/users/santama/add-yandex-certificates-into-a-java-keystore/) your local java.
  
#### YDB
[YDB_TOKEN](https://ydb.yandex-team.ru/docs/getting_started/start_auth#autentifikaciya) should be set in environment 
#### S3
[S3_ACCESS_KEY and S3_SECRET](https://wiki.yandex-team.ru/vertis/howto/mds-s3-howto/#poluchenieaccesskey) should be set in environment 
### Teamcity
[Builds](https://t.vertis.yandex-team.ru/project/VerticalsBackend_EtcMono_Palma?mode=builds)
### Metrics
[Palma API](https://grafana.vertis.yandex-team.ru/d/l_JqoP3Zz/palma)
### Alerts
### Logs
[Logs](https://admin.vertis.yandex-team.ru/logs?layer=test&period=2h&limit=100&service=palma-api&branch=)


