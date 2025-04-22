Script using for add users to mongo-databases through mongos:

examples:
add user test1 to unstable db taxi with RO privileges for all collections:
  `add-mongo-user.py -u test1 -d taxi -p read -e unstable`

add user test1 to testing db taxi, collection test_col, RW privileges:
  `add-mongo-user.py -u test1 -d taxi -p readWrite -e testing -c test_col`

add user test1 to all environments, db taxi, collection test_col, RW privileges and add secrets to strongbox:
  `add-mongo-user.py -u test1 -d taxi -p readWrite -c test_col --to-strongbox -s taxi_infra`

help:
```
usage: add-mongo-user.py [-h] -u USER -d DATABASE -p {read,readWrite}                         [--to-strongbox] [-s SERVICE]                         [-e ENVIRONMENT [ENVIRONMENT ...]] [-c COLLECTION]
                         [--mongo-params MONGO_PARAMS]

Tools to create mongodb user

optional arguments:
  -h, --help            show this help message and exit
  -u USER, --user USER  User
  -d DATABASE, --database DATABASE
                        Database
  -p {read,readWrite}, --permission {read,readWrite}
                        Permission for user, may be read or readWrite
  --to-strongbox        Add mongo-connection secret to strongbox. Required
                        --service parameter.
  -s SERVICE, --service SERVICE
                        Name of service that requested the user
  -e ENVIRONMENT [ENVIRONMENT ...], --environment ENVIRONMENT [ENVIRONMENT ...]
                        Can be unstable, testing, stable. By default used all
                        environment
  -c COLLECTION, --collection COLLECTION
                        Collection
  --mongo-params MONGO_PARAMS
                        Optional. Additional mongo parameters using in
                        connection string for strongbox.
                        mongodb://<user>:<password>@<port>/<dbname>[?<mongo-
                        params>]
```
