## How to build docker image and upload to AWS registry.

1. Build docker image:
    ```
    export VERS=$(arc describe --svn | head -c 8)_<version_description>
    ya package pkg.json --custom-version $VERS --docker

    export IMAGE=582601430203.dkr.ecr.us-east-2.amazonaws.com/solver-integration-tests:$VERS
    docker tag registry.yandex.net/solver-integration-tests:$VERS $IMAGE
    ```

2. Upload image to AWS registry:

    2.1 Login to docker registry.
    Steps described in [backend docker readme](./../../async_backend/aws_docker/readme.md)

    2.2 Then push image:
    ```
    docker push $IMAGE
    ```
