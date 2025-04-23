To build:

```
ya make -j0 --checkout
ya make
```

To run local tests:

```
ya make -t -j0 --checkout
ya make -t
```

To build package:

```
ya package package.json --docker --docker-repository paysys-test
```

To run mongo integration tests

```
sudo docker-compose up
sudo docker exec -it mongoidm_mongo-idm_1 useradd -m -u $(getent passwd ${USER} | cut -f 3 -d ':') ${USER}
sudo docker exec --user ${USER} -it mongoidm_mongo-idm_1 bash
cd /arcadia/paysys/sre/apps/mongo_idm/
```

And run the tests as usual.

For test yav integration add yav token to environment variables.

```
export YAV_OAUTH_TOKEN="xxx"
```
