# VM Scheduler in AWS (Server part)

## Kubernetes
Secret: vm-scheduler
ConfigMap: vm-scheduler
Deployment: vm-scheduler
Service: vm-scheduler (tcp port 50001)

[More info](https://a.yandex-team.ru/arc/trunk/arcadia/maps/b2bgeo/vm_scheduler/k8s/readme.md)

## Repository
[Docker image repository](https://us-east-2.console.aws.amazon.com/ecr/repositories/private/582601430203/vm-scheduler?region=us-east-2)

## Database
[Primary database](https://us-east-2.console.aws.amazon.com/rds/home?region=us-east-2#database:id=vm-scheduler-postgres;is-cluster=false) has one sync replica in another availability zone (`Multi-AZ = Yes`).

[Replica database](https://us-east-2.console.aws.amazon.com/rds/home?region=us-east-2#database:id=vm-scheduler-postgres-replica;is-cluster=false)

[Secret](https://us-east-2.console.aws.amazon.com/secretsmanager/home?region=us-east-2#!/secret?name=vm-scheduler%2Fpostgres) with primary database credentials. Replica uses same user and password.

[YAV-Secret](https://yav.yandex-team.ru/secret/sec-01fzdts4qbqqn44gg2tfjpvtf5)

## Logs
[vmscheduler](https://us-east-2.console.aws.amazon.com/cloudwatch/home?region=us-east-2#logsV2:log-groups/log-group/vmscheduler)

## How to create grpc request

1. Publish service to k8s (read maps/b2bgeo/vm_scheduler/k8s/readme.md)
2. Install grpcurl:
https://github.com/fullstorydev/grpcurl#installation
3. Mount arcadia
4. cd to arcadia with vm-scheduler proto:
```
cd <path to arcadia root>/maps/b2bgeo/vm_scheduler/proto/services
```
5. Setup port-forwardking (kubectl should be configured to interact with cluster)
```
kubectl port-forward deployment/vm-scheduler 50001:50001 -n stable
```
6. Make request with grpcurl
```
grpcurl -plaintext -import-path <PATH TO ARCADIA ROOT> -proto public_api.proto localhost:50001 maps.b2bgeo.vm_scheduler.proto.PublicApiScheduler/healthCheck
```
7. For more complex requests see:
https://github.com/fullstorydev/grpcurl
