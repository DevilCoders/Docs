# Warn: do not run docker from icar! (or any other qyp instance)

----

## Build container
```bash
cd ~/arcadia/maps/b2bgeo/analytics
source deploy/aws/build.sh

# to check built images you can run
docker image list
```

## Deploy container locally
```bash
docker run -td --name routeq-analytics-aws routeq-analytics
```
Some explanation to  arguments
```
-t: Allocate a pseudo-TTY (i.e Do not stop container if there is no entrypoint)
-d: Run container in background and print container ID
routeq-analytics-aws - name of container (process)
routeq-analytics - name of image
```

## Run scripts
We can run scripts inside container running. Just select the container and type command.<br/>
Note: for now most of the commands will not work in aws ec2 instance, because they need yandex-team internal network.
  But they will work from your own laptop. Ba careful testing them
```bash
docker exec routeq-analytics-aws vrp-billing --help
```

You can also connect to shell inside container with the following command
```bash
docker exec -it routeq-analytics-aws bash
```

## Deploy container in aws

Here is some instructions for steps 4,5,3 (yes, in that order)<br/>
https://blog.clairvoyantsoft.com/deploy-and-run-docker-images-on-aws-ecs-85a17a073281

**1) Get aws account**<br/>
Just write @sapaeff

**2) Upload ssh keys to amazon**<br/>
TODO: I did not understand this part and how to upload your own key.
For now, we can do following:<br/>
If you are allocating new instance, you can just create new key on next step.<br/>
Otherwise, you can ask someone with access to add you key<br/>

**3) Spawn aws ec2 instance**<br/>
TODO: Automatic upload of ssh keys.
TODO: configuring DNS.

Probably, instance is already spawned, and you need to somehow upload you public key to it.<br/>
For now  just ask @sapaeff to add it manually<br/>
And add your key to s3 bucket. Later I will configure automatic key sync with ec2 instance
```
aws s3 cp "~/.ssh/id_rsa.pub" "s3://routeq-analytics/infra/ssh-keys/$(whoami)"
```

If you really need to spawn new instance just go to aws console UI and create it.<br/>
For testing purpose you can just spawn t2.micro. All setting are default, except os image, please select `ubuntu`

You can connect to created instance by the following command
```bash
ssh -i <path-to-ssh-key> ubuntu@<public-ip-or-dns-name>
# Example
ssh -i ~/.ssh/sapaeff-test-rsa.pem ubuntu@ec2-18-217-53-116.us-east-2.compute.amazonaws.com
```

You may want to create user `robot-b2bgeo` or some other users.<br/>
TODO: some instructions to help with first configuration of new instance

**4) Create container registry**<br/>
Done. For now, I think single container image registry is enough.<br/>
Our registry: `582601430203.dkr.ecr.us-east-2.amazonaws.com`<br/>
https://us-east-2.console.aws.amazon.com/ecr/repositories/private/582601430203/analytics?region=us-east-2

Go to https://582601430203.signin.aws.amazon.com/console. Register a new __service_key__ there.

**5) Upload image to registry:**<br/>
```bash
# First time, you need to save you credentials
aws configure
# Put your service_key here

aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 582601430203.dkr.ecr.us-east-2.amazonaws.com
# You should see `Login Succeeded`

# docker tag is just setting alias for image. Then docker push decides by this name, where is remote image registry located.
# It is required to call image /<ecr-name>:<any-tag>. In our case ecr-name = analytics. Tag - you can chose any.
docker tag routeq-analytics 582601430203.dkr.ecr.us-east-2.amazonaws.com/analytics:latest
docker push 582601430203.dkr.ecr.us-east-2.amazonaws.com/analytics:latest
```

**6) Elastic container storage**<br/>
TODO: Too hard. Maybe better to ask backend. I did not understand this part.<br/>
This is required for some convenient regular deployment of containers.<br/>
You need to first make task-description.<br/>
Then you need service.<br/>
Then ??

**7) Pull docker image from aws ec2 instance**<br/>
From inside ec2 instance:
```bash
sudo apt update
sudo apt install docker.io awscli
aws configure
sudo chmod 666 /var/run/docker.sock # костыль?
aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 582601430203.dkr.ecr.us-east-2.amazonaws.com
docker pull 582601430203.dkr.ecr.us-east-2.amazonaws.com/analytics:latest
```

**8) Deploy container**<br/>
For now - the same as deploying you local container
You may also want to tag it first.
```bash
docker tag 582601430203.dkr.ecr.us-east-2.amazonaws.com/analytics routeq-analytics
docker run -td --name routeq-analytics-aws routeq-analytics
# Probably this name is busy so you can use another one
docker exec -it routeq-analytics-aws bash # to test something from inside container
```

## Deploy cron in aws
The same as local cron.<br/>
For now, the easiest way is to write `crontab -e` and paste `./deploy/aws/crontab` file.
