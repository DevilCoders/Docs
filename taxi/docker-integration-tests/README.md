# Integration tests

##Wiki
More comprehensive information is available on wiki:
https://wiki.yandex-team.ru/taxi/backend/docker-integration-tests/

## Login to docker distribution service
For this you need to get any OAuth token issued in Yandex.
You can get token by following the link: 
https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1

After you must run the following command:

    docker login -u <login> registry.yandex.net

Where you can type OAuth token.

For more information about this, see the wiki: 
https://wiki.yandex-team.ru/cocaine/docker-registry-distribution/#avtorizacija

## Run tests

Run `make tests-prepare` to initialize database and setup environment. Then
run `docker-compose run --rm taxi-tests` to start pytest.

You can also run `pytest` directly with options of your choice:

    docker-compose run --rm taxi-tests pytest -t 10 taxi-tests/tests/main/test_launch.py -vvs

When something goes wrong run `make tests-prepare` and try again. If it does
not help try `make clean` instead.

To run tests during (tests) development, you may do this first:

    docker-compose run --rm taxi-tests bash
   
And then run selected tests repeatedly inside this container:

    root@6b8baba0546c:/taxi# pytest -t 10 taxi-tests/tests/main/test_launch.py -k test_no_phone -vvs
    
This will use most recent sources from mounted host directory.

## Check local code

You can also test your c++ code. To do this, put the symbolic
link `backend-cpp` in the root directory.

You can also test your python code. To do this, put the symbolic
link `backend` in the root directory.

## Interaction with containers

You can run the admin panel, admin panel 2.0, kibana, and access them
from your host. In addition, you can access the protocol handlers using
curl or mobile application. To do this you must run:

    make run-taxi-proxy

Services will be opened on the following ports:
* 80   - taxi-tc (client and protocol)
* 8080 - taxi-admin
* 8000 - tariff-editor (admin 2.0)
* 8800 - kibana

To connect a mobile application on android you must run:

    make client-mode

At this time you can't run tests.

## Run linters/formatters (need [taxi-deps-py3](https://github.yandex-team.ru/taxi/deps-py3#installation))

#### Run in all repository / run only on changed files
* `make check-pep8`  / `make smart-check-pep8` - python linter
* `make format` / `make smart-format` - taxi formatter

## Add new service to integration tests
To add a new service to integration tests just run the following command with your parameters.

    scripts/add_service.py <service-name> <repo_name> [--rtc]

After that you can change the created files and configure them in appropriate way

Main article: https://wiki.yandex-team.ru/taxi/backend/docker-integration-tests/#podkljuchenienovogomikroservisa
