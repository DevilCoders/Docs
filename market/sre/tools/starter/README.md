# Starter
> A unified "endpoint" for starting an application in Nanny. It knows about ports, directories, limits and how to launch applications.

## Rotation of Hprof files
Nanny does not provide an embedded solution for rotation hprof files. It is why starter rotates them.
How does it work?
1. If it is a container without volumes then will be called a simple rotation by "number of files". By default, no more than 2 files should be left. 
2. If it is a container with volumes then will be called a rotation by "available space". By "available space" states the following. An application will not be started if there is not available space for at least one hprof file.

In the second case, as the size of hprof file is used the amount of guaranteed memory.

## Usage example
```
root@vla1-4710-cae-vla-market-test--0f5-10907:/place/db/iss3/instances/10907_testing_market_cpp_test_service_vla_D62qU2rF5NI# BSCONFIG_IPORT_PLUS_1=80 BSCONFIG_IPORT_PLUS_2=81 bin/starter --app-name cpp-test-service --dry-run
/place/db/iss3/instances/10907_testing_market_cpp_test_service_vla_D62qU2rF5NI/bin/cpp-test-service-start.sh --logdir=/var/logs/yandex/cpp-test-service --httpport=80 --debugport=81 --tmpdir=/place/db/iss3/instances/10907_testing_market_cpp_test_service_vla_D62qU2rF5NI/tmp --datadir=/persistent-data/cpp-test-service --extdatadir=/place/db/iss3/instances/10907_testing_market_cpp_test_service_vla_D62qU2rF5NI/data-getter --environment=testing --dc=vla --cpu-count=1
root@vla1-4710-cae-vla-market-test--0f5-10907:/place/db/iss3/instances/10907_testing_market_cpp_test_service_vla_D62qU2rF5NI#
```

In services it is configured in `Instance Spec`, e.g. `bin/starter --app-type cpp --app-name {INSTANCECTL_CONTAINER}`

## Links
Motivation is here https://st.yandex-team.ru/CSADMIN-28199
