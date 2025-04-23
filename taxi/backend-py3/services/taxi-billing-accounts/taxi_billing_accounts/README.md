###

* [wiki](https://wiki.yandex-team.ru/taxi/backend/billing/accounts)

### Loadtest install snippet

```
#!/usr/bin/env bash

sudo apt-get update; \
sudo apt-get install yandex-taxi-billing-accounts && \
sudo systemctl daemon-reload && \
sudo systemctl restart yandex-taxi-billing-accounts-master.target && \
sudo systemctl restart nginx && \
curl -v http://xenial-target.taxi.load.yandex.net/ping
```

### Running tests
```
git clone git@github.yandex-team.ru:bekbulatov/docker-backend-py3.git
cd docker-backend-py3
GIT_TAXI_BACKEND_PATH=~/dev/backend-py3 ./run taxi-driver-partner-test /usr/lib/yandex/taxi-py3-2/bin/py.test -vv -x --no-postgresql --no-redis --no-indexes --mongo=mongodb://mongo:27017/test_ ./tests/billing_accounts
```


### Running server
* Run ...
```
GIT_TAXI_BACKEND_PATH=~/dev/backend-py3 ./run taxi-driver-partner-test bash
/usr/lib/yandex/taxi-py3-2/bin/python3.7 -m taxi_billing_accounts.app --path /tmp/taxi_billing_accounts_0.sock --instance 0
```
* Test ...
```
docker exec -it $(docker ps | grep taxi-xenial3 | awk '{print $1}') bash
printf 'GET /ping HTTP/1.0\r\n\r\n' | nc -q 2 -U /tmp/taxi_billing_accounts_0.sock
```
* Flake8
```
PATH="${PATH}:/usr/lib/yandex/taxi-py3-2/bin/" ./tools/checkpep8
```

## Info

* Task for service creation: [TAXIADMIN-4024](https://st.yandex-team.ru/TAXIADMIN-4024)
