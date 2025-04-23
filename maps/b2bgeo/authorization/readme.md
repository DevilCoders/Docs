# Authorization service

## Balancer
[External application balancer](https://us-east-2.console.aws.amazon.com/ec2/v2/home?region=us-east-2#LoadBalancers:sort=loadBalancerName) (Name: routing)

[Security-group](https://us-east-2.console.aws.amazon.com/ec2/v2/home?region=us-east-2#SecurityGroups:search=sg-06736f4d31b50b366;sort=group-id) allows traffic from any to 443 via HTTPS

Balancer fqdn: `routing-967715551.us-east-2.elb.amazonaws.com`

DNS record: `routing-967715551.us-east-2.elb.amazonaws.com CNAME api.yandex-routing.com`
DNS record: `routing-967715551.us-east-2.elb.amazonaws.com CNAME api.routeq.com`

[Certificates](https://us-east-2.console.aws.amazon.com/ec2/v2/home?region=us-east-2#ELBCertificates:type=app;loadBalancerName=routing;loadBalancerId=f2ad7340c4f970e0;listenerId=acfdf0ba60c3b551;accountId=582601430203) for `*.yandex-routing.com`, `*.routeq.com`

[Routing](https://us-east-2.console.aws.amazon.com/ec2/v2/home?region=us-east-2#ELBRules:type=app;loadBalancerName=routing;loadBalancerId=f2ad7340c4f970e0;listenerId=acfdf0ba60c3b551;accountId=582601430203): forwards all requests to authotization fargate service.

[Apikey to signature secret](https://us-east-2.console.aws.amazon.com/secretsmanager/home?region=us-east-2#!/secret?name=solver%2Fapikey_to_signature) must be stored in `APIKEY_TO_HTTP_SIGNATURE_KEY` env var.

[Company id to apikey (testing)](https://us-east-2.console.aws.amazon.com/secretsmanager/home?region=us-east-2#!/secret?name=testing%2Fauthorization%2Fcompany-to-apikey) must be stored in `APIKEY_TO_HTTP_SIGNATURE_KEY` env var.

[Company id to apikey (stable)](https://us-east-2.console.aws.amazon.com/secretsmanager/home?region=us-east-2#!/secret?name=stable%2Fauthorization%2Fcompany-to-apikey) must be stored in `APIKEY_TO_HTTP_SIGNATURE_KEY` env var.

## Fargate service
[Authorization fargate service](https://us-east-2.console.aws.amazon.com/ecs/home?region=us-east-2#/clusters/default/services/authorization-service/details)

[Security group](https://us-east-2.console.aws.amazon.com/vpc/home?region=us-east-2#SecurityGroup:groupId=sg-06c60b001193d08dc) allows traffic: from [external application balancer](https://us-east-2.console.aws.amazon.com/ec2/v2/home?region=us-east-2#LoadBalancers:sort=loadBalancerName) to 80 via HTTP

[Docker image repository](https://us-east-2.console.aws.amazon.com/ecr/repositories/private/582601430203/authorization?region=us-east-2)

[Task definition](https://us-east-2.console.aws.amazon.com/ecs/home?region=us-east-2#/taskDefinitions/authorization-service-task-definition)

## How to access Fargate container
1. [already done] Allow service to execute commands
```
aws ecs update-service --cluster default --enable-execute-command --service authorization-service
```
2. [already done] Add `ssmmessages` policy to task execution role
3. [already done] Deploy service
4. Connect to task
```
aws ecs execute-command --cluster default --task TASK_ID --container authorization-service --interactive --command "/bin/sh"
```

## How to create signed request

1. Build `generate_signature` tool:
```
arcadia/maps/b2bgeo/libs/signature/tools $ ya make -r
```
2. Take apikey and secret from [AWS Secrets Manager](https://us-east-2.console.aws.amazon.com/secretsmanager/home?region=us-east-2#!/secret?name=solver%2Fapikey_to_signature). Format: AWS_SOLVER_APIKEY:AWS_SOLVER_SECRET_KEY
3. Generate signature:
```
# set AWS_SOLVER_APIKEY and AWS_SOLVER_SECRET_KEY env vars

./generate_signature -a "curl" -m "POST" -u "/vrs/api/v1/add/svrp?apikey="$(echo $AWS_SOLVER_APIKEY) -b '{"depot":{"id":"100","point":{"lat":55.799087,"lon":37.729377},"time_window":"07:00-23:59"},"locations":[{"id":"location","point":{"lat":55.781803,"lon":37.708392},"time_window":"09:00-18:00"}],"options":{"date":"2021-02-09","time_zone":3.0,"matrix_router":"geodesic"},"vehicle":{"id":1}}' -k $AWS_SOLVER_SECRET_KEY
```
4. Make request:
```
# store signature from previous step in AWS_SOLVER_SIGNATURE env var

curl "https://api.routeq.com:/vrs/api/v1/add/svrp?apikey="$(echo $AWS_SOLVER_APIKEY)  -X POST -i -H "X-YaCourier-Signature: "$(echo $AWS_SOLVER_SIGNATURE) -d '{"depot":{"id":"100","point":{"lat":55.799087,"lon":37.729377},"time_window":"07:00-23:59"},"locations":[{"id":"location","point":{"lat":55.781803,"lon":37.708392},"time_window":"09:00-18:00"}],"options":{"date":"2021-02-09","time_zone":3.0,"matrix_router":"geodesic"},"vehicle":{"id":1}}' -H "User-Agent: curl"
```

## Deployment

### Docker publishing

```
cd aws_docker

# Open push.sh and set $VERS with your tag then:
sh push.sh
```

### k8s deploy

Before deployment, set docker tag from previous commands to deployment.yaml

```
cd k8s

# Deploy to stable
sh apply-stable.sh

# Deploy to testing
sh apply-testing.sh
```
