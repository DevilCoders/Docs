# Build

Try to build actual image:
`docker-compose build` or `make build`

As result you're received:

    $ docker images
    REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
    yandex-l3mgr-celery-beat     latest              8a63eda39024        20 minutes ago      688MB
    yandex-l3mgr-celery-worker   latest              bd931d467b32        20 minutes ago      688MB
    yandex-l3mgr-uwsgi           latest              d720d55acc44        20 minutes ago      688MB
    yandex-l3mgr-base            latest              08787a0db3d3        20 minutes ago      688MB
    ubuntu                       focal               1e4467b07108        3 weeks ago         73.9MB

- docker_uwsgi: contains uwsgi and start workers from uwsgi.ini configuration.
- docker_celery-beat: runs only one celery beat process
- docker_celery-worker: runs 12 workers, that process all l3manager tasks

# Docker Registry authentication

For uploading image into the internal registry will need to
authenticate (https://wiki.yandex-team.ru/qloud/docker-registry/#authorization)

1. Generate OAuth token for the
   registry. [Just visit link](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1)
2. Enter login command
   `$ docker login -u yushkovsky --password-stdin registry.yandex.net`
   enter received in the first step token and press `^D`

Example:

        $  docker login -u yushkovsky --password-stdin registry.yandex.net
        AQAD-XXXX
        WARNING! Your password will be stored unencrypted in /home/yushkovsky/.docker/config.json.
        Configure a credential helper to remove this warning. See
        https://docs.docker.com/engine/reference/commandline/login/#credentials-store

        Login Succeeded

# Deployment actions

For easier deployment Makefile has been written, that support basically events:

- build new images (base and services):

        make build

- build with specified TAG for service images:

        TAG=20210129-0 make build

- run services

        make up

- stop all services

        make down

- stop all services with specified timeout value in seconds

        TIMEOUT=60 make down

Default values for exist flags:

- TAG = latest
- TIMEOUT = 180

Base actions workflow might be presented as:

        export TAG=20210201-0

        make build
        make push

        make pull
        TIMEOUT=120 make down
        make up

# Test actions

Currently, to run tests You need to do the following:

       make test

It will spawn postgres database and run tests on it.

