## Projects description

Service to deliver events to different storages (yt, kafka, clickhouse)

[Chat](https://t.me/joinchat/Rf9HXqHOdA99-meG)

[Documentation](https://docs.yandex-team.ru/classifieds-infra/broker/info)

[Api](../../../schema-registry/proto/broker/api/broker.proto)

 
Request queue: https://st.yandex-team.ru/createTicket?type=2&priority=2&queue=VSDATA 

## Dev space

### Databases and storages
 * [logbroker](https://lb.yandex-team.ru/docs/)
 * [yt](https://yt.yandex-team.ru/docs/)
 
### Balancer
Broker needs quite high number of in-flight requests. Much higher than average service. 
So it was decided to make dedicated envoy installation (see [VERTISADMIN-24304](https://st.yandex-team.ru/VERTISADMIN-24304) for more details)

Address: **broker-api-lb-http.query.consul:80**. It's metrics are [here](https://grafana.vertis.yandex-team.ru/d/4Vx3-GqWk/broker-api-lb?viewPanel=6&orgId=1&refresh=1m&var-Datasource=Prometheus&var-DC=All&var-version=All&var-allocation_id=All&var-cluster=broker-api-grpc&var-rate=1m&var-percentile=0.9&from=now-6h&to=now)

To access from a host without consul agent: **broker-api-grpc-api.vrts-slb.test.vertis.yandex.net:80**

Alternative way is to go to broker directly via consul dns: **broker-api-grpc-api.query.consul**. 
It has advantages in resilience to node failures: grpc retries request to different node.
While in case of consul it retries to consul which still might try a failed node.  
 
### Branching 

## Services

### How to run locally

To run components that use yt or lb locally you need to get auth token respective service. See service documentation.
 
### Metrics
[Broker API](https://grafana.vertis.yandex-team.ru/d/ybtbWWaZz/broker-api)
### Alerts
### Logs
[Grafana](https://grafana.vertis.yandex-team.ru/s/t/Fa_A4hgf4QxCKP)
