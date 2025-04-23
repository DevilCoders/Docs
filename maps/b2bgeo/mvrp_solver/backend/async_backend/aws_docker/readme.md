# Asynchronous Solver in AWS

## Balancer
[Internal application balancer](https://us-east-2.console.aws.amazon.com/ec2/v2/home?region=us-east-2#LoadBalancers:sort=loadBalancerName) (Name: solver)

[Security-group](https://us-east-2.console.aws.amazon.com/ec2/v2/home?region=us-east-2#SecurityGroups:search=sg-04115d644e8c2f084;sort=group-id)
allows traffic from [routing balancer](https://us-east-2.console.aws.amazon.com/ec2/v2/home?region=us-east-2#LoadBalancers:sort=loadBalancerName) to 80 via HTTP

Balancer fqdn: `internal-solver-227200320.us-east-2.elb.amazonaws.com`

[Routing](https://us-east-2.console.aws.amazon.com/ec2/v2/home?region=us-east-2#ELBRules:type=app;loadBalancerName=solver;loadBalancerId=3db6ed3cc4d11468;listenerId=88fac34ee29189c5;accountId=582601430203): forwards all requests to async-solver service.


## Service
[Async-solver service with on-demand instances](https://us-east-2.console.aws.amazon.com/ecs/home?region=us-east-2#/clusters/default/services/async-solver/details)

[Security group](https://us-east-2.console.aws.amazon.com/vpc/home?region=us-east-2#SecurityGroup:groupId=sg-03901467d1402acd0) allows traffic: from [internal solver balancer](https://us-east-2.console.aws.amazon.com/ec2/v2/home?region=us-east-2#LoadBalancers:sort=loadBalancerName) to 80 via HTTP

[Docker image repository](https://us-east-2.console.aws.amazon.com/ecr/repositories/private/582601430203/async-solver?region=us-east-2)

[Task definition](https://us-east-2.console.aws.amazon.com/ecs/home?region=us-east-2#/taskDefinitions/async-solver-task-definition/status/ACTIVE)

[Placement group](https://us-east-2.console.aws.amazon.com/ec2/v2/home?region=us-east-2#PlacementGroups:) (Name: async-solver-spread)

[Auto scaling group](https://us-east-2.console.aws.amazon.com/ec2autoscaling/home?region=us-east-2#/details/async-solver?view=details)

## Database
[Primary database](https://us-east-2.console.aws.amazon.com/rds/home?ad=c&cp=bn&p=rdsp&region=us-east-2#database:id=solver-postgres;is-cluster=false;tab=connectivity) has one sync replica in another availability zone (`Multi-AZ = Yes`).

[Replica database](https://us-east-2.console.aws.amazon.com/rds/home?ad=c&cp=bn&p=rdsp&region=us-east-2#database:id=solver-postgres-replica;is-cluster=false)

[Secret](https://us-east-2.console.aws.amazon.com/secretsmanager/home?region=us-east-2#!/secret?name=postgres-solver) with primary database credentials. Replica uses same user and password.

## S3 Storage
[S3 bucket](https://s3.console.aws.amazon.com/s3/buckets/yandex-asyncsolver-default?region=us-east-2&tab=objects)

[Secret](https://us-east-2.console.aws.amazon.com/secretsmanager/home?region=us-east-2#!/secret?name=s3-storage) stores S3 bucket credentials.

[VPC Endpoints](https://us-east-2.console.aws.amazon.com/vpc/home?region=us-east-2#Endpoints:sort=vpcEndpointId). Here must be configured Gateway endpoint for `service com.amazonaws.\[s3 region\].s3`

## CloudWatch Logs
[CloudWatch log groups](https://us-east-2.console.aws.amazon.com/cloudwatch/home?region=us-east-2#logsV2:log-groups)

[CloudWatch asyncsolver log group](https://us-east-2.console.aws.amazon.com/cloudwatch/home?region=us-east-2#logsV2:log-groups/log-group/asyncsolver)

[async-solver.log](https://us-east-2.console.aws.amazon.com/cloudwatch/home?region=us-east-2#logsV2:log-groups/log-group/asyncsolver/log-events/async-solver.log)

[nginx-access-tskv.log](https://us-east-2.console.aws.amazon.com/cloudwatch/home?region=us-east-2#logsV2:log-groups/log-group/asyncsolver/log-events/nginx-access-tskv.log)

[nginx-error.log](https://us-east-2.console.aws.amazon.com/cloudwatch/home?region=us-east-2#logsV2:log-groups/log-group/asyncsolver/log-events/nginx-error.log)

## Metrics

[Grafana](https://g-a4c40d6f07.grafana-workspace.us-east-2.amazonaws.com/d/eovZL6Lnz/async-solver)
To view grafana you need to assign your AWS SSO user to grafana in [control panel](https://us-east-2.console.aws.amazon.com/grafana/home?region=us-east-2#/workspaces/g-a4c40d6f07/SSOConfiguration). If you need to edit a dashboard, you must be assigned as an Admin. ATTENTION: for each Admin we pay twice as much as for Viewer, so there must be serious reasons to grant you Admin role.
Also, we have uptime checks in [Grafana](https://g-a4c40d6f07.grafana-workspace.us-east-2.amazonaws.com/d/zIQ_zhu7z/solver-uptime?orgId=1&from=now-7d&to=now)

## How to build docker image and upload to AWS registry.

1. Build package:
    ```
    export VERS=my_test_version
    ya package pkg.json --custom-version $VERS
    ```
2. Build docker image:
    ```
    export IMAGE=582601430203.dkr.ecr.us-east-2.amazonaws.com/async-solver:$VERS
    docker build --network host -t $IMAGE - < b2bgeo-asyncsolver.$VERS.tar.gz
    ```
    May be command "docker" must be run with "sudo"
3. Upload image to AWS registry:

    3.0 We need to make sure that the ssh key is installed, if not, do following:
    ```
    eval `ssh-agent -s`
    ssh-add ~/.ssh/[your key]
    ```
    3.1 Install AWS cli: https://aws.amazon.com/cli/

    3.2 Configure AWS
    ```
    aws configure set aws_access_key_id $(ya vault get version sec-01fcxga20786whdheyw65gba4f -o access-key-id)
    aws configure set aws_secret_access_key $(ya vault get version sec-01fcxga20786whdheyw65gba4f -o secret-access-key)
    aws configure set default.region us-east-2
    aws configure set default.output json
    ```

    3.3 Authenticate Docker to an Amazon ECR private registry
    ```
    sudo aws ecr get-login-password --region us-east-2 | sudo docker login --username AWS --password-stdin 582601430203.dkr.ecr.us-east-2.amazonaws.com
    ```

    3.4 Push image
    ```
    sudo docker push $IMAGE
    ```
